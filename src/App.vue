<template>
    <div class='py-4 container'>
        <TitleList :theme_dark="theme_dark" :title='title_special' :description='description_special'
            :src_user='src_user' />
        <TasksList :theme_dark="theme_dark" @check="checked" :tasks='tasks' />
        <NavBar :theme_dark="theme_dark" @delete_tasks="delete_tasks" @update_description="update_description"
            @update_title="update_title" @dark_mode="dark_mode" @delete_auto="delete_auto" @add_task="add_task"
            :title='title' :description='description' :delete_auto_check='delete_auto_check' />
    </div>
</template>

<script>
import TitleList from './components/ListTitle.vue'
import TasksList from './components/TasksList.vue'
import NavBar from './components/NavBar.vue'
// so vem vagabunda
export default {
    name: 'App',
    components: {
        TitleList,
        TasksList,
        NavBar,
    },
    data() {
        return {
            // header
            title: 'Lista de Tarefas',
            description: 'Como é bom ter uma vida mais organizada',
            src_user: '../assets/img/users/user_default.png',

            // tasks
            tasks: [],

            // functionalities
            delete_auto_check: true,
            theme_dark: false,
        }
    },
    methods: {
        add_task(item) {
            this.tasks.push({
                title: item, checked: false
            })
        },
        delete_tasks() {
            this.tasks = []
        },
        delete_auto() {
            (this.delete_auto_check == true) ? this.delete_auto_check = false : this.delete_auto_check = true
            console.log('delete_auto', this.delete_auto_check)
        },
        dark_mode() {
            (this.theme_dark == true) ? this.theme_dark = false : this.theme_dark = true
            document.querySelector('body').classList.toggle('bg-dark')
            document.querySelector('hr').classList.toggle('bg-white')
        },
        checked(index) {
            if (this.delete_auto_check == true) {

                setTimeout(() => {
                    if (this.delete_auto_check == true) {
                        this.tasks.splice(parseInt(index), 1)
                    }
                }, 400)
            }
        },
        update_description(value) {
            this.description = value
        },
        update_title(value) {
            this.title = value
        }
    },
    computed: {
        title_special() {
            if (this.title.length > 20) {
                return this.title.slice(0, 19) + '...'
            } else {
                return this.title
            }
        },
        description_special() {
            if (this.description.length > 88) {
                return this.description.slice(0, 87) + '...'
            } else {
                return this.description
            }
        },
    }
}

</script>

<style>
input,
textarea,
input:focus,
textarea:focus {
    border-radius: 15px !important;
    outline: 0;
    resize: none;
    background: dotted;
}

.container {
    max-width: 100%;
    margin: 0 auto;
}

/* ---- resposividade ---- */

@media screen and (min-width:375px) {

    /* -- img user -- */
    .header .img_user {
        max-width: 100%;
    }

    /* -- title -- */
    .h2_title {
        padding-left: 0;
        background-color: transparent;
    }

    .p_title {
        padding-left: 0;
    }

    /* -- navbar -- */
    .div_add_task .div_btn_close {
        width: 3rem;
        height: 3rem;
        padding: .5em;
    }

    .div_add_task .div_btn_add {
        width: 3rem;
        height: 3rem;
        padding: .5em;
    }

    .div_add_task .div_icon_config {
        position: relative;
        width: 3rem;
        height: 3rem;
        padding: .58em .69em .69em .69em;
    }
}

@media screen and (min-width:425px) {

    /* -- img user -- */
    .header .img_user {
        max-width: 70%;
    }

}

@media screen and (min-width:768px) {

    /* -- img user -- */
    .header .img_user {
        max-width: 50%;
    }

    /* -- title -- */
    .header .h2_title {
        font-weight: 800;
        font-size: 1.6em;
        border: none;
        width: 100%;
    }

    .header .p_title {
        color: #3f97af;
        font-weight: 500;
        font-size: .9em;
    }

    /* -- navbar -- */
    .div_add_task .div_btn_close {
        width: 3.5rem;
        height: 3.5rem;
        padding: .65em;
    }

    .div_add_task .div_btn_add {
        width: 3.5rem;
        height: 3.5rem;
        padding: .6em;
    }

    .div_add_task .div_icon_config {
        position: relative;
        width: 3.5rem;
        height: 3.5rem;
        padding: .85em .88em .88em .88em;
    }
}
@media screen and (min-width:768px) {
    /* -- img user -- */
    .header .img_user {
        max-width: 30%;
    }

    /* -- title -- */
    .header .h2_title {
        font-weight: 800;
        font-size: 4em;
        border: none;
        width: 100%;
    }

    .header .p_title {
        color: #3f97af;
        font-weight: 500;
        font-size: 1.5em;
    }
}
</style>
