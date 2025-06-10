<template>
    <div class="text-white h-auto w-screen bg-black p-5">
        <form id="register" method="POST" class="p-5 border-3 border-green-400 shadow-lg text-black block sm:1/2 md:w-1/3 rounded-md bg-gradient-to-t from-green-400 to-blue-400">

            <p class="text-4xl font-bold">Register</p>
            
            <div class="pb-4">
                <label for="usernameRegister" class="text-md block">Username</label>
                <input
                type="text"
                id="usernameRegister"
                name="usernameRegister"
                class="text-sm rounded py-1 text-white mb-2 px-2 focus:outline-none bg-black border border-black"
                placeholder='Your username'
                required>
    
                <label for="passwordRegister" class="text-md block">Password</label>
                <input
                type="password"
                id="passwordRegister"
                name="passwordRegister"
                class="text-sm rounded py-1 text-white mb-2 px-2 focus:outline-none bg-black border border-black"
                placeholder='Your password'
                required>

                <label for="cPasswordRegister" class="text-md block">Confirm Password</label>
                <input
                type="password"
                id="cPasswordRegister"
                name="cPasswordRegister"
                class="text-sm rounded py-1 text-white mb-2 px-2 focus:outline-none bg-black border border-black"
                placeholder='Confirm your password'
                required>

                <button class="mt-3 rounded-md w-20 block text-white bg-black">Submit</button>
            </div>
        </form>


        <form id="login" method="POST" class="mt-6 p-5 border-3 border-green-400 shadow-lg text-black block sm:1/2 md:w-1/3 rounded-md bg-gradient-to-t from-green-400 to-blue-400">
            
            <p class="text-4xl font-bold">Login</p>

            <div class="pb-4">
                <label for="usernameLogin" class="text-md block">Username</label>
                <input
                type="text"
                id="usernameLogin"
                name="usernameLogin"
                class="text-sm rounded py-1 text-white mb-2 px-2 focus:outline-none bg-black border border-black"
                placeholder='Your username'
                required>
    
                <label for="passwordLogin" class="text-md block">Password</label>
                <input
                type="password"
                id="passwordLogin"
                name="passwordLogin"
                class="text-sm rounded py-1 text-white mb-2 px-2 focus:outline-none bg-black border border-black"
                placeholder='Your password'
                required>

                <button class="mt-3 rounded-md w-20 block text-white bg-black">Submit</button>
            </div>
        </form>
    </div>
</template>