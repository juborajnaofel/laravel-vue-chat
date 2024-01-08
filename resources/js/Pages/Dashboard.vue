<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, useForm, usePage } from '@inertiajs/vue3';
import { ref } from 'vue';

const currentUser = ref(usePage()?.props?.auth?.user.id);
const currentChatRoomID = ref(null);


const form = useForm({
    message: null,
    chat_room_id: null,
});

const onChatRoomSelect = (id) => {
    currentChatRoomID.value = id;
    form.chat_room_id = id;
}
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Chat Room</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="flex flex-row p-3">
                        <div class="w-1/4 bg-slate-200 p-2">
                            Chat Rooms
                            <div class="h-[600px] overflow-auto">
                                <span v-for="item in [1,2,3,4,5,6,7,8, 9, 10,11]" @click="onChatRoomSelect(item)">
                                    <div class="flex flex-row bg-slate-300 rounded-md p-3 m-3" :class="currentChatRoomID == item? ' bg-slate-600':''" >
                                        {{ item }}
                                    </div>
                                </span>
                            </div>

                        </div>
                        <div class="w-3/4 h-[600px] p-2">
                            <div class="flex flex-col">
                                <div class="h-[550px] overflow-auto">
                                    <span v-for="item in [{message:1, user_id: 1} ,{message:2, user_id:1}, {message:3, user_id:3}]">
                                        <div class="m-3" v-if="item.user_id !== currentUser">
                                            <div class="flex flex-row">
                                                <div class="w-3/4 bg-slate-200 rounded-md p-3">
                                                    {{ item.message }}
                                                </div>
                                            </div>
                                        </div>
                                        <div class="m-3" v-else>
                                            <div class="flex flex-row justify-end ">
                                                <div class="w-3/4 bg-slate-200 rounded-md p-3">
                                                    {{ item.message }}
                                                </div>
                                            </div>
                                        </div>
                                    </span>
                                </div>
                                <div class="h-[50px]">
                                    <form action="">
                                        <div class="flex flex-row">
                                            <input v-model="form.message" type="text" class="w-5/6 rounded-md"/>
                                            <button class="w-1/6 bg-slate-200 rounded-md">Send</button>
                                        </div>
                                    </form>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
