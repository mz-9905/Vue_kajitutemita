<template>
    <div id="app" class=".container">
        <div class="p-3 text-center">
            <h1>{{appName}}</h1>
        </div>
        <p class="p-3">
            <span>Total:{{total}}</span>
            <span>: </span>
            <button v-on:click="sort(-1)" class="btn btn-primary">降順</button>
            <span>⇔</span>
            <button v-on:click="sort(1)" class="btn btn-primary">昇順</button>
            <span> : </span>
            <button v-on:click="reset()" class="btn btn-primary">Reset</button>
            <span> : </span>
            <select v-model="f_type" v-on:change="filterType()" class="dropdown">
                <option></option>
                <option v-for="type in m_type">{{type}}</option>
            </select>
        </p>
        <ShowList :array="results"/>
    </div>
</template>

<script>
import ShowList from './components/ShowList.vue'

const C_URL="https://docs.google.com/spreadsheets/d/e/2PACX-1vTyDY0c4wb2qJ0VtUzTDJnH7tvv_e0Iao1PKIV46E_wQM5cImcSGWQWX1GrylkqENDi-v0B-Yw7eDqG/pub?gid=0&single=true&output=csv";

const myData = {
    appName: "ポケモン全国図鑑(一部抜粋)",//アプリ名
    pokemon: null,//JSONファイルから読み込んだデータを格納
    results: null,//"pokemon"からの抽出データを格納
    m_type: null,//typeセレクタの要素を格納
    f_type: null,//typeセレクタで選択した値を格納
    total: 0//抽出したデータの総数
}

export default{
    name:"App",
    data(){//扱うデータ
        return myData;
    },
    created(){//起動時に自動実行
        //Axiosを使ってファイルを読み込む
        const vue = this;//重要
        const option={responseType: "blob"};
        axios.get(C_URL, option).then(res=>{//Google SpreadSheetからデータ取得
            res.data.text().then(str=>{vue.init(str);});//文字列→JSONオブジェクト
        });
    },
    methods:{//関数一覧(実行されるごとに再計算)
        init(str){
            this.pokemon=this.csv2json(str).pokemon;//文字列をJSON形式に変換,"pokemon"に格納
            this.m_type=new Set();
            for(let poke of this.pokemon){
                if(poke.type.length>0){
                    for(let type of poke.type.split("_")) this.m_type.add(type);
                };
            };
            this.reset();
        },
        reset(){//表示をデータ読み込み直後の状態にリセット
            this.results=this.pokemon;//resultsにコピー
            this.f_type="";//typeセレクタをリセット
            this.total=this.results.length;//現時点のresultsの総数
        },
        sort(num){//データを降順/昇順でソート
            this.results.sort((a,b)=>{
                if(a.index.length<=0||b.index.length<=0) return 0;
                return (Number(a.index)-Number(b.index))*num;
            });
        },
        filterType(){//セレクタで選択したtypeのみ表示
            const type=this.f_type;//セレクタで選択した値
            this.results=this.pokemon.filter(poke=>{
                //typeの文字列がpoke.typeに含まれているか確認
                if(type.length>0 && !poke.type.includes(type)) return false;
                return true;
            });
            this.total=this.results.length;
        },
        csv2json(str){
            const json={pokemon:[]};//JSONオブジェクトを用意
            const rows=str.split("\r\n");//改行区切りで1件づつに分割
            const keys=rows[0].split(",");//1行目はデータの種類(カラム)
            for(let i=1;i<rows.length;i++){//2行目以降のデータを扱う
                const cells=rows[i].split(",");//","カンマ区切りで分割
                const obj=new Object();//1件のオブジェクトを生成
                for(let j=0;j<keys.length;j++) obj[keys[j]]=cells[j];//キーとバリューでオブジェクトに追加
                json.pokemon.push(obj);//JSONオブジェクトに追加
            }
            return json;//JSONオブジェクトを返す
        }
    },
    components:{ ShowList }
}
</script>
