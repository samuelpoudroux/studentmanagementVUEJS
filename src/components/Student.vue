<template>
<div>
    <h1>{{ me.firstname }} {{ me.lastname }}</h1>
        <input type="text" placeholder="firstname" v-model="me.firstname">
        <input type="text" placeholder="lastname" v-model="me.lastname">
            <button v-on:click="updateStudent">update</button>
        <button v-on:click="deleteStudent">delete</button>
</div>
</template>

<script>

export default {
    name: 'Student',
    data() {
        return {
            me: {},
        }
    },
    props: {
        myURL: String,
    },
    methods: {
        getMe: function () {
            fetch("http://api-students.popschool-lens.fr" + this.myURL)
            .then(r => r.json())
            .then(r => {
                // console.log(r)
                this.me = r;
            })
        },

        updateStudent: function(){
             console.log(this.me.firstname + "deleted")

            fetch("http://api-students.popschool-lens.fr/api/students" + this.me.id, {
            headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json'
            },
            method: "PUT",
            
            body: JSON.stringify({
                firstname: this.me.firstname,
                lastname: this.me.lastname
               
            })
        })

        },

        deleteStudent: function(){

             console.log(this.me.firstname + "deleted")
            
            fetch("http://api-students.popschool-lens.fr/api/students/" + this.me.id, {
           
            method: "DELETE",
            
            })
        },
    },
    mounted () {
        this.getMe()

    }
};

 </script>

<style scoped>

    .studentitem{
  display: block;
  background-color: #9eff44;
  margin: 10px 50px; padding: 15px 5px;
    }

    h1{
        color: red;
    }

</style>