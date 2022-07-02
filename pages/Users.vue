<template>
    <div>
        <Header />
        <div class="users">
            <div class="user" v-for="user in users" :key="user.userId">
                <div>
                    <h1>{{user.name}}</h1>
                    <h3>{{user.username}}</h3>
                    <p>{{user.email}}</p>
                    <p>{{user.address.street}}</p>
                    <p>{{user.address.suite}}</p>
                    <p>{{user.address.city}}</p>
                    <p>{{user.address.zipcode}}</p>
                    <p>{{user.address.geo.lat}}{{user.address.geo.lng}}</p> 
                </div>
                <div>
                    <ul>
                        <li v-for="userPost in getPostlistByUserId(user.id)" :key="userPost.id">
                            {{userPost.title}}
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
// get deta from server
    components: {Header},
    data(){
        return{
            urlPosts: 'https://jsonplaceholder.typicode.com/posts',
            urlUsers: 'https://jsonplaceholder.typicode.com/users',
            posts: [],
            users:[],
            userName:'',
            userPosts:[],
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
            },
            getPostlistByUserId(userId) {
                // let foundUser = this.users.find(user => user.id == postUserId)
                // this.userName = foundUser.name;

                let filteredPosts = this.posts.filter(post => post.userId == userId)
                return filteredPosts
            }
    },
}
</script>


<style>
.users {
    width: 90%;
    margin-left: auto;
    margin-right: auto;
}
.user{
    margin: 1rem auto;
    padding: 1rem;
    background: rgba(214, 213, 213, 0.603);
    border: 1px solid rgba(41, 170, 225, 0.548);
}
</style>