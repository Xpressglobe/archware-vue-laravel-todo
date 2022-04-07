<template>
    <div class="mt-3">
        <h2>Please Add Tasks</h2>
        <div class="container m-2 w-100">
            <small class="error">{{this.msg}}</small><br>
            <input
                type="text"
                placeholder="add item"
                class="border"
                v-model="item.name"
            />
            <br>
             <input
                type="text"
                placeholder="add category"
                class="border"
                v-model="item.category"
            />
            <br>
            <button
                :class="[item.name ? 'active' : 'notactive']"
                @click="addItem()"
            >
               Click to add Item    <font-awesome-icon icon="plus-square"
               />
            </button>
        </div>
    </div>
</template>
<script>
export default {
    data: function() {
        return {
            item: {
                name: "",
                category:"",

            },
        msg:""
        };
    },
    methods: {
        addItem() {
            if (this.item.name == "") {
                return;
            }
            if (this.item.category == "") {
                return;
            }
            axios
                .post("api/item/store", {
                    item: this.item
                })
                .then(res => {
                    console.log(res);
                    if (res.status == 200) {
                        this.item.name = "";
                        this.item.category = "";
                        this.msg=res.data;

                        this.$emit("reloadlist");
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        }
    }
};
</script>

<style scoped>
.active {
    color: white;
    background-color: blue;
}
.inactive {
    color: gray;
}
.error{
    color: red;

}
.border{
    border: 1px solid black;
}
</style>
