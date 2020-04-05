<template>
    <div class = "main">
        <SideMenu
            :isAdmin          = "isAdmin"
            :visible          = "visible"
            :progress         = "personalProgress"
            :total            = "total"
            @switchMain     = "switchMain"
            @switchStat     = "switchStat"
            @switchSettings = "switchSettings"
        />
        <div class = "content">
            <Marking
                :listOfGroup="listOfGroup"
                :count="count"
                :generalStat="generalStat"
                :personalStat="personalStat"
                :personalProgress="personalProgress"
                :generalProgress="generalProgress"
                :total="total"
                @next="next"
                v-if = "visible ==='Main'"
            />
            <Stat
                :generalStat="generalStat"
                :personalStat="personalStat"
                :adminStat="adminStat"
                :personalProgress="personalProgress"
                :generalProgress="generalProgress"
                :total="total"
                :isAdmin="isAdmin"
                v-if = "visible ==='Stat'"
            />
            <Settings
                :list="generalStat"
                @up="up"
                @down="down"
                @save="save"
                @add="add"
                @del="del"
                @cancel="loaderData"
                v-if = "visible ==='Settings'"
            />
        </div>
    </div>
</template>

<script>
import SideMenu from './SideMenu.vue';
import Marking from './Marking.vue';
import Stat from './Stat.vue';
import Settings from './Settings.vue';
export default {
    name      : "Main",
    components: {
        SideMenu,
        Marking,
        Stat,
        Settings,
    },
    data(){
        return {
            listOfGroup : [],
            count       : 0,
            adminStat   : [],
            generalStat : [],
            personalStat: [],

            personalProgress: 0,
            generalProgress : 0,
            total           : 0,

            isAdmin: false,
            visible: 'Main',
        }
    },
    beforeCreate(){
        this.$http.post(
            "http://abitbot.cloud.nstu.ru/markup/get_sample/",
            {},
            {
                headers: {
                    'Authorization': 'Bearer '+ sessionStorage.jwt
                }
            }
        ).then(function(response) {
            this.adminStat        = response.body.admin_stat;
            this.listOfGroup      = response.body.questions;
            this.personalProgress = response.body.stat.markup_stat.local;
            this.total            = response.body.stat.markup_stat.total;
            this.generalProgress  = response.body.stat.markup_stat.global;
            this.generalStat      = response.body.stat.marks_stat.global.sort((a,b)=>{return a.priority-b.priority});
            this.personalStat     = response.body.stat.marks_stat.local.sort((a,b)=>{return a.priority-b.priority});
            this.isAdmin          = response.body.is_admin
            for (var i = 0; i < this.listOfGroup.length; i++) {
                this.listOfGroup[i].type = 0;
            }
            console.log(this.adminStat)
        }, function() {
            alert("В доступе отказано")
            this.$router.push({name: "Login"})
        })
    },
    methods:{
        loaderData(){
            this.$http.post(
                "http://abitbot.cloud.nstu.ru/markup/get_sample/",
                {},
                {
                    headers: {
                        'Authorization': 'Bearer '+ sessionStorage.jwt
                    }
                }
            ).then(function(response) {
                this.isAdmin          = response.body.is_admin
                this.adminStat        = response.body.admin_stat;
                this.listOfGroup      = response.body.questions;
                this.personalProgress = response.body.stat.markup_stat.local;
                this.total            = response.body.stat.markup_stat.total;
                this.generalProgress  = response.body.stat.markup_stat.global;
                this.generalStat      = response.body.stat.marks_stat.global.sort((a,b)=>{return a.priority-b.priority});
                this.personalStat     = response.body.stat.marks_stat.local.sort((a,b)=>{return a.priority-b.priority});
                for (var i = 0; i < this.listOfGroup.length; i++) {
                    this.listOfGroup[i].type = 0;
                }
            }, function() {
                alert("В доступе отказано")
                this.$router.push({name: "Login"})
            })
        },
        switchMain(){
            this.visible = 'Main';
        },
        switchStat(){
            this.visible = 'Stat';
        },
        switchSettings(){
            this.visible = 'Settings';
        },
        next(){
            this.count = 0;
            for (var i = 0; i < this.listOfGroup.length; i++)
                if (this.listOfGroup[i].type === 0) this.count++;
            console.log(this.count)
            if(this.count > 0){
                alert("Не размечено " + this.count + " вопросов!");
            }
            else{
                this.$http.post(
                    "http://abitbot.cloud.nstu.ru/markup/add_class/",
                    {
                        mas: this.listOfGroup
                    },
                    {
                        headers: {
                            'Authorization': 'Bearer '+ sessionStorage.jwt
                        }
                    }
                ).then(function() {
                    this.loaderData();
                }, function() {
                    alert("В доступе отказано")
                    this.$router.push({name: "Login"})
                })
            }
        },
        del(id){
            this.$http.post(
                "http://abitbot.cloud.nstu.ru/markup/delete_mark/",
                {
                    id: id
                },
                {
                    headers: {
                    'Authorization': 'Bearer '+ sessionStorage.jwt
                    }
                }
            ).then(function() {
                this.loaderData();
            }, function() {
                this.$router.push({name: "Login"})
                alert("В доступе отказано")
            })
        },
        up(priority) {
            if (priority != 0)
            {
                this.generalStat[priority].priority--
                this.generalStat[priority-1].priority++
                var temp = this.generalStat[priority]
                this.generalStat[priority] = this.generalStat[priority-1]
                this.generalStat[priority-1] = temp
            }
        },
        down(priority) {
            if (priority != this.generalStat.length-1)
            {
                this.generalStat[priority].priority++
                this.generalStat[priority+1].priority--
                var temp = this.generalStat[priority]
                this.generalStat[priority] = this.generalStat[priority+1]
                this.generalStat[priority+1] = temp
            }
        },
        save(){
            var temp = []
            for (var i = 0; i < this.generalStat.length; i++)
                temp.push({id: this.generalStat[i].mark_id, priority: this.generalStat[i].priority})
            this.$http.post(
                "http://abitbot.cloud.nstu.ru/markup/set_priority/",
                {
                    marks: temp
                },
                {
                    headers: {
                    'Authorization': 'Bearer '+ sessionStorage.jwt
                    }
                }
            ).then(function() {
                this.loaderData();
            }, function() {
                this.$router.push({name: "Login"})
                alert("В доступе отказано")
            })
        },
        add(name){
            this.$http.post(
                "http://abitbot.cloud.nstu.ru/markup/mark/",
                {
                    mark: {name: name}
                },
                {
                    headers: {
                    'Authorization': 'Bearer '+ sessionStorage.jwt
                    }
                }
            ).then(function() {
                this.loaderData();
            }, function() {
                this.$router.push({name: "Login"})
                alert("В доступе отказано")
            })
        },
    }
}
</script>

<style scoped>
.content{
    width   : 85vw;
    position: fixed;
    top     : 0;
    right   : 0;
    margin  : 20px 20px 0 0;
}
</style>