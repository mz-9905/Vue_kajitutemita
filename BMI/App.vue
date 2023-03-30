<template>
    <div id="app" class=".container">
        <ShowResults :appName="appName" :message="message" :cm="cm" :kg="kg" :bmi="bmi" />
        <div class="p-3 mb-3 col-4">
            <label for="i_cm" class="form-label">身長(cm)</label>
            <input v-model="cm" type="text" class="form-control" id="i_cm">
            <div class="form-text">身長を入力してください(cm)</div>
        </div>
        <div class="p-3 mb-3 col-4">
            <label for="i_kg" class="form-label">体重(kg)</label>
            <input v-model="kg" type="text" class="form-control" id="i_kg">
            <div class="form-text">体重を入力してください(kg)</div>
        </div>
        <div class="mb-3 d-grid gap-2 col-6 mx-auto">
            <button v-on:click="calc" class="btn btn-primary">計算</button>
        </div>
        <JudgeBMI :bmi="bmi"/>
    </div>
</template>

<script>
import ShowResults from './components/ShowResults.vue'
import JudgeBMI from './components/JudgeBMI.vue';

const myData = {
    appName: "BMI 計算機",//アプリ名
    message: "身長と体重を入力してください",//メッセージ
    cm: 160,//身長
    kg: 60,//体重
    bmi: 0//BMI値
}

export default{
    name:"App",
    data(){//扱うデータ
        return myData;
    },
    created(){//起動時に自動実行
        this.calc();
    },
    methods:{//関数一覧
        calc(){//BMI計算
            this.bmi=this.kg/((this.cm*0.01)**2);//計算式
        }
    },
    components:{ ShowResults, JudgeBMI }
}
</script>
