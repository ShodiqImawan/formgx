<template>
    <!-- Container Utama -->
    <div class="min-h-screen bg-black text-white flex flex-col md:flex-row p-5 space-y-8 md:space-y-0 md:space-x-8 justify-center items-start">

        <!-- Container Form -->
        <div class="w-full md:w-1/2 flex flex-col items-center space-y-6">
            <!-- Form Sign Up -->
            <form id="signup"  @submit.prevent="signupUser" method="POST" class="w-full max-w-sm p-6 border border-green-400 shadow-lg rounded-md bg-gradient-to-t from-green-400 to-blue-400 text-black">
    
                <p class="text-4xl font-bold">Sign Up</p>
                
                <div class="pb-4">
                    <label for="usernameSignup" class="text-md block">Username</label>
                    <input
                    type="text"
                    id="usernameSignup"
                    name="usernameSignup"
                    class="text-sm rounded py-1 text-white mb-2 px-2 focus:outline-none bg-black border border-black"
                    placeholder='Your username'
                    required>
        
                    <label for="passwordSignup" class="text-md block">Password</label>
                    <input
                    type="password"
                    id="passwordSignup"
                    name="passwordSignup"
                    class="text-sm rounded py-1 text-white mb-2 px-2 focus:outline-none bg-black border border-black"
                    placeholder='Your password'
                    required>
    
                    <label for="cpasswordSignup" class="text-md block">Confirm Password</label>
                    <input
                    type="password"
                    id="cpasswordSignup"
                    name="cpasswordSignup"
                    class="text-sm rounded py-1 text-white mb-2 px-2 focus:outline-none bg-black border border-black"
                    placeholder='Confirm your password'
                    required>
                    
                    <!-- Submit Sign Up -->
                    <button class="mt-3 rounded-md w-20 block text-white bg-black">Submit</button>
                </div>
            </form>
    
            <!-- Form Sign In -->
            <form id="signin" @submit.prevent="signinUser" method="POST" class="mt-6 w-full max-w-sm p-6 border border-green-400 shadow-lg rounded-md bg-gradient-to-t from-green-400 to-blue-400 text-black">
                
                <p class="text-4xl font-bold">Sign In</p>
    
                <div class="pb-4">
                    <label for="usernameSignin" class="text-md block">Username</label>
                    <input
                    type="text"
                    id="usernameSignin"
                    name="usernameSignin"
                    class="text-sm rounded py-1 text-white mb-2 px-2 focus:outline-none bg-black border border-black"
                    placeholder='Your username'
                    required>
        
                    <label for="passwordSignin" class="text-md block">Password</label>
                    <input
                    type="password"
                    id="passwordSignin"
                    name="passwordSignin"
                    class="text-sm rounded py-1 text-white mb-2 px-2 focus:outline-none bg-black border border-black"
                    placeholder='Your password'
                    required>
    
                    <button class="mt-3 rounded-md w-20 block text-white bg-black">Submit</button>
                </div>
            </form>
        </div> <!-- Ujung Container Form -->

        <!-- Container Menampilkan Data -->
        <div class="w-full md:w-1/2 flex flex-col items-center space-y-4 flex-1">
            <div class="w-full min-h-[400px] md:min-h-[620px] md:mr-4 lg:mr-7 my-2 p-4 overflow-y-auto scrollbar-track-transparent max-h-[400px] md:max-h-[620px] rounded-md bg-amber-200 relative">
                <!-- Jika belum ada data -->
                <div v-if="user.length === 0" class="absolute inset-0 flex items-center justify-center">
                    <p class="text-center text-xl font-bold text-black block">
                        Belum ada data pengguna.
                    </p>
                </div>
                
                <!-- Sample -->
                <div v-for="u in user" :key="u.id" class=" w-full bg-black text-white p-3 rounded-md shadow-md mb-2">
                    <div class="flex justify-between items-center">
                        <p class="font-semibold">{{ u.username }}</p>
                        <button @click="deleteUser(u.id, u.username)" class="px-3 py-1 bg-red-500 text-white rounded hover:bg-red-600 transition">Hapus</button>
                    </div>  
                </div>


            </div>
        </div>
    </div>
</template>

<script>
    export default{
        mounted() {
            fetch('https://portugal-extent-merge-treasurer.trycloudflare.com/get')
            .then(res => res.json())
            .then(data => {
                this.user = data;
            })
            .catch(err => {
                console.error('Gagal ambil data:', err);
            });
        },
        methods: {
            deleteUser(id, username) {
                fetch('https://portugal-extent-merge-treasurer.trycloudflare.com/delete', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        id: id,
                        username: username
                    })
                })
                .then(res => {
                    if (!res.ok) {
                        return res.json().then(err => {throw new Error(err.detail);});
                    }

                    return res.json()
                })
                .then(data => {
                    alert(data.msg);
                    this.getData();
                })
                .catch(err => {
                    alert(`Gagal: ${err.message}`)
                })
            },
            getData() {
                fetch('https://portugal-extent-merge-treasurer.trycloudflare.com/get')
                .then(res => res.json())
                .then(data => {
                    this.user = data;
                })
                .catch(err => {
                    console.error('Gagal ambil data: ', err);
                })
            },
            signupUser() {
                const username = document.getElementById('usernameSignup').value;
                const password = document.getElementById('passwordSignup').value;
                const cpassword = document.getElementById('cpasswordSignup').value;

                if (password !== cpassword) {
                    alert('Password tidak cocok')
                    return
                }

                fetch('https://portugal-extent-merge-treasurer.trycloudflare.com/signup', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        username: username,
                        password: password,
                        cpassword: cpassword
                    })
                })
                .then(res => {
                    if (!res.ok) {
                        return res.json().then(err => { throw new Error(err.detail);});
                    }

                    return res.json()
                })
                .then(data => {
                    alert(data.msg);
                    this.getData();
                })
                .catch(err => {
                    alert(`Gagal: ${err.message}`)
                })
            },
            signinUser() {
                const username = document.getElementById('usernameSignin').value;
                const password = document.getElementById('passwordSignin').value;

                fetch('https://portugal-extent-merge-treasurer.trycloudflare.com/signin', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        username: username,
                        password: password
                    })
                })
                .then(res => {
                    if (!res.ok) {
                        return res.json().then(err => {throw new Error(err.detail);});
                    }

                    return res.json()
                })
                .then(data => {
                    alert(data.msg);
                    this.getData();
                })
                .catch(err => {
                    alert(`Gagal: ${err.message}`)
                })
            }
        },
        data() {
            return {
                user: []
            }
        }
    }
</script>