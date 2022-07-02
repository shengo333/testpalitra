<template>
    <div>
        <Header />
        <div class="posts">
                <div class="post" v-for="post in posts" :key="post.id">
                    <router-link :to="{ path: '/post/' + post.id}">
                    <!-- <router-link to="/Post"> -->
                        <h2>{{post.title}}</h2>
                    </router-link>
                    <p>{{post.body}}</p>
                    <li>
                        {{getUserNameById(post.userId)}}
                    </li>
                </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import Header from './Header.vue'
export default {

    components: {Header},
    data(){
        return{
            urlPosts: 'https://jsonplaceholder.typicode.com/posts',
            urlUsers: 'https://jsonplaceholder.typicode.com/users',
            posts: [],
            users:[],
            userName:'',
        }
    },
    mounted(){
        this.getData();
        this.getUsers();
    },
    methods:{
        async getData(){
            const response = await axios.get(this.urlPosts);
            console.log(response);
            this.posts = response.data;
        },
        async getUsers(){
            const response = await axios.get(this.urlUsers);
            console.log(response);
            this.users = response.data;
            console.log(this.users)
        },
        getUserNameById(postUserId) {
            let foundUser = this.users.find(user => user.id == postUserId)
            if(foundUser){
                return foundUser.name
            }
        },
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
</style>