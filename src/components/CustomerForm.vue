<template>
    <div class="customer-form">
        <div v-for="(customer, index) in customers" :key="customer.id" class="customer-row">
            <div class="row-header">
                <span class="row-number">旅客{{ index + 1 }}</span>
                <button type="button" @click="removeCustomer(index)"><i class="fa fa-times" aria-hidden="true"></i></button>
            </div>
            <div class="input-fields">
                <div class="input-field">
                    <label>姓名</label>
                    <input type="text" size="6" v-model="customer.name" @input="updateHiddenInput" />
                </div>
                <div class="input-field">
                    <label>身分證字號</label>
                    <input type="text" size="10" v-model="customer.idNumber" @input="updateHiddenInput" />
                </div>
                <div class="input-field">
                    <label>生日(西元)</label>
                    <input class="field-passengerbirth" type="date" :max="maxDate" v-model="customer.birthday" @input="updateHiddenInput" />
                </div>
                <div class="input-field">
                    <label>身高(cm)</label>
                    <input type="number" size="6" v-model="customer.height" @input="updateHiddenInput" />
                </div>
                <div class="input-field">
                    <label>體重(kg)</label>
                    <input type="number" size="6" v-model="customer.weight" @input="updateHiddenInput" />
                </div>
                <div class="input-field">
                    <label>鞋號(cm)</label>
                    <input type="number" size="6" v-model="customer.shoeSize" @input="updateHiddenInput" />
                </div>
            </div>
        </div>
        <input type="hidden" class="input-text" name="billing_text_by_jq" id="billing_text_by_jq" placeholder=""
            :value="hiddenInputValue">
        <button type="button" class="add_field_button" @click="addCustomer"><i class="fa fa-plus" aria-hidden="true"></i>增加旅客資料</button>
    </div>
</template>

<script>
export default {
    name: 'CustomerForm',
    data() {
        return {
            maxDate: new Date().toISOString().substr(0, 10),
            hiddenInputValue: '',
            customers: [
                { id: 1, name: '', idNumber: '', birthday: '', height: '', weight: '', shoeSize: '' },
                { id: 2, name: '', idNumber: '', birthday: '', height: '', weight: '', shoeSize: '' },
                { id: 3, name: '', idNumber: '', birthday: '', height: '', weight: '', shoeSize: '' },
            ],
        };
    }, methods: {
        updateHiddenInput() {
            const customersData = this.customers.map((customer, index) => {
                return `${index + 1}. ${customer.name} ${customer.idNumber} ${customer.birthday} 身高${customer.height} 體重${customer.weight} 鞋號${customer.shoeSize}`;
            });

            this.hiddenInputValue = customersData.join(',');
        },
        addCustomer() {
            const newCustomer = {
                id: Date.now(),
                name: '',
                idNumber: '',
                birthday: '',
                height: '',
                weight: '',
                shoeSize: '',
            };
            this.customers.push(newCustomer);
        },
        removeCustomer(index) {
            if (index > 0) {
                this.customers.splice(index, 1);
                this.updateHiddenInput();
            }
        },
    },
};
</script>