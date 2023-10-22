<template>
  <div class="usertable-container">
    <div class="usertable">
      <h1>User Search</h1>
      <div class="form__group">
        <input class = "form__field" v-model="searchUsername" placeholder="Username"/>
        <input class = "form__field" v-model="searchEmail" placeholder="Email" />
        <button class="search_button" @click="searchUsers">Search</button>
        <button class="reset_button" @click="loadUsers">X</button>
      </div>
      <div v-if="isDataLoaded">
        <UserTable :columns="columns" :rows="rows" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import UserTable from './UserTable.vue';

export default {
  name: 'HomePage',
  data() {
    return {
        columns: [
          {
            label: 'Username',
            field: 'username', 
          },
          {
            label: 'Email',
            field: 'email',
          },
          {
            label: 'Description',
            field: 'description'
          },
          {
            label: 'Address', 
            field: 'address' 
          }
        ],
        rows: [],
        firstRender: true,
      searchUsername: '',
      searchEmail: '',  
    };
  },
  components: {
    UserTable
  },
  created() {
    this.loadUsers();
  },
  computed: {
  isDataLoaded() {
      return this.rows.length!=0 || !this.firstRender;
    }
  },
  watch: {
    isDataLoaded: {
      deep: true,
      handler: function () {
        this.firstRender = false;
      }
    }
  },
  methods: {
    async loadUsers() {
      try {
        const response = await axios.get(process.env.VUE_APP_BASE);
        const userArray = response.data.body.map(user => {
          // Map the fields you need from the response to your user object
          return {
            username: user.username,
            address: user.address,
            description: user.description,
            email: user.email,
          };
        });
        this.rows = userArray;
      } catch (error) {
        console.error('Error searching users:', error);
      }
    },
    async searchUsers() {
      try {
        // Send a POST request with the search parameters
        const response = await axios.post(process.env.VUE_APP_BASE, {
            "body": {
              username: this.searchUsername,
              email: this.searchEmail
          }
        });
        const userArray = response.data.body.map(user => {
          return {
            username: user.username,
            address: user.address,
            description: user.description,
            email: user.email,
          };
        });
        this.rows = userArray;
      } catch (error) {
        console.error('Error searching users:', error);
      }
    },
  },
};
</script>

<style>
.search_button {
  cursor: pointer;
  outline: 0;
  color: #fff;
  background-color: #0d6efd;
  border-color: #0d6efd;
  display: inline-block;
  font-weight: 400;
  line-height: 1.5;
  text-align: center;
  border: 1px solid transparent;
  padding: 6px 12px;
  font-size: 16px;
  border-radius: .25rem;
  transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
  :hover {
      color: #fff;
      background-color: #0b5ed7;
      border-color: #0a58ca;
  }            
}

.reset_button {
  cursor: pointer;
  outline: 0;
  color: #fff;
  background-color: #b64747;
  border-color: #b64747;
  display: inline-block;
  font-weight: 400;
  line-height: 1.5;
  text-align: center;
  border: 1px solid transparent;
  padding: 6px 12px;
  font-size: 16px;
  border-radius: .25rem;
  transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
  :hover {
      color: #fff;
      background-color: #0b5ed7;
      border-color: #0a58ca;
  }            
}


.form__group {
  position: relative;
  padding: 15px 0 0;
  margin-top: 10px;
  width: 50%;
  display: flex;
  flex-direction: row;
}
.usertable-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  font-family: 'Poppins', sans-serif; 
  background-color:#ffffff;
}

.form__field {
  font-family: inherit;
  border: 0;
  border-bottom: 2px solid gray;
  outline: 0;
  font-size: 1.3rem;
  color: rgb(25, 16, 107);
  padding: 7px 0;
  background: transparent;
  transition: border-color 0.2s;

  &::placeholder {
    color: transparent;
  }

  &:placeholder-shown ~ .form__label {
    font-size: 1.3rem;
    cursor: text;
    top: 20px;
  }
}

.form__label {
  position: absolute;
  top: 0;
  display: block;
  transition: 0.2s;
  font-size: 1rem;
  color: gray;
}

.form__field:focus {
  ~ .form__label {
    position: absolute;
    top: 0;
    display: block;
    transition: 0.2s;
    font-size: 1rem;
    color: primary;
    font-weight:700;    
  }
  padding-bottom: 6px;  
  font-weight: 700;
  border-width: 3px;
  border-image: linear-gradient(to right, primary,secondary);
  border-image-slice: 1;
}
/* reset input */
.form__field{
  &:required,&:invalid { box-shadow:none; }
}


</style>