<template>
    <div class=".container">
        <div class="p-3 text-center">
            <table class="table table-bordered table-striped-columns">
                <thead>
                    <tr>
                        <th>図鑑番号</th>
                        <th>名前</th>
                        <th>タイプ</th>
                        <th>進化前</th>
                        <th>進化後</th>
                        <th>特性</th>
                        <th>HP</th>
                        <th>こうげき</th>
                        <th>ぼうぎょ</th>
                        <th>とくこう</th>
                        <th>とくぼう</th>
                        <th>すばやさ</th>
                        <th>合計</th>
                    </tr>
                    <tr v-for="item in array">
                        <td>{{item.index}}</td>
                        <td>{{item.name}}</td>
                        <td><p v-for="split_type in splitUnderbar(item.type)">{{split_type}}</p></td>
                        <td><p v-for="split_before in splitUnderbar(item.before)">{{split_before}}</p></td>
                        <td><p v-for="split_after in splitUnderbar(item.after)">{{split_after}}</p></td>
                        <td><p v-for="split_ability in splitUnderbar(item.ability)">{{split_ability}}</p></td>
                        <td>{{item.hp}}</td>
                        <td>{{item.a}}</td>
                        <td>{{item.b}}</td>
                        <td>{{item.c}}</td>
                        <td>{{item.d}}</td>
                        <td>{{item.s}}</td>
                        <td>{{item.all}}</td>
                    </tr>
                </thead>
            </table>
        </div>
    </div>
</template>
<script>
export default({
    props:['array'],
    methods:{
        splitUnderbar(str){//文字列を"_"で分割,各文字を格納した配列を返す
            let arr=[];//分割した文字を格納
            for(let chr of str.split("_")) arr.push(chr);//文字列を"_"で分割
            console.log(arr)
            return arr;
        }
    }
})
</script>

<style scoped>
table{
    font-size: 0.8em;
}
td{
    text-align: center;
    vertical-align: middle;
}
</style>