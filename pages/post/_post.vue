<template>
    <div>
        <div class="posts">
                <div class="post">
                    <h1>{{post.title}}</h1>
                    <p>{{post.body}}</p>
                    <p> {{getUserNameById(post.userId)}}</p>
                    {{userName.email}}
                    <button @click="showFiveComents = !showFiveComents">Toggle coments</button>
                </div> 
                <div class="coments">
                    <div v-if="showFiveComents">
                        <div v-for="(coment, index) in coments" :key="coment">
                            <div class="coment" v-show="index < 5">
                                <p>{{coment.name}}</p>
                                <p>{{coment.email}}</p>
                                <p>{{coment.body}}</p>
                            </div>
                        </div>
                    </div>
                    <div v-if="!showFiveComents">
                        <div v-for="(coment, index) in coments" :key="coment">
                            <div class="coment">
                                <p>{{coment.name}}</p>
                                <p>{{coment.email}}</p>
                                <p>{{coment.body}}</p>
                            </div>
                        </div>
                    </div>
                </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {

    data(){
        return{
            urlPosts: 'https://jsonplaceholder.typicode.com/posts/' + this.$route.params.post,
            urlUsers: 'https://jsonplaceholder.typicode.com/users',
            urlComents: 'https://jsonplaceholder.typicode.com/comments',
            coments: [],
            posts: [],
            users:[],
            userName:'',
            post:{},
            showFiveComents: true
        }
    },
    mounted(){
        this.getData();
        this.getUsers();
        this.getComents();
    },
    methods:{
        async getData(){
            const response = await axios.get(this.urlPosts);
            this.post = response.data;
        },
        async getUsers(){
            const response = await axios.get(this.urlUsers);
            this.users = response.data;
            console.log(this.users)
        },
        getUserNameById(postUserId) {
            let foundUser = this.users.find(user => user.id == postUserId)
            if(foundUser){
                this.userName = foundUser
                return foundUser.name
            }
        },
        async getComents(){
            const response = await axios.get(this.urlComents);
            console.log(response);
            this.coments = response.data;
            console.log(this.coments)
        }

    }
}
</script>

<style>
body{
    margin: 0;
}

.page-enter-active,
.page-leave-active {
  transition: opacity 0.5s;
}
.page-enter,
.page-leave-to {
  opacity: 0;
}

.post{
    width: 80%;
    padding: 1rem;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid gray;
    margin: 1rem auto;
    background: rgb(235, 232, 232);
}
.post a{
    text-transform: none;
    text-decoration: none;
    color: rgba(41, 170, 225);;
    font-size: bold;
}
.coment{
    width: 40%;
    padding: 1rem;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid rgb(161, 161, 161);
    margin: 1rem auto;
    background: rgb(175, 123, 123);
}
</style>