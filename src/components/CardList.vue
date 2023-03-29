<template>
    <article>
        <ul class="cardList">
            <li class="card" v-for="item in items" :key="item.id">
                <div class="cardHeader">
                    <p>{{ item.title }}</p>
                </div>
                <div class="cardBody">
                    <p>{{ item.text }}</p>
                </div>
            </li>
        </ul>
    </article>
</template>

<script setup lang="ts">
//item數量較少沒有跟lists切成兩個componet
const items: { id: number, title: string, text: string }[] = [
    { id: 1, title: '外觀', text: '白頭鵯體長約17到22公分，額至頭頂純黑色而富有光澤，兩眼上方至後枕白色，形成一白色枕環。耳羽後部有一白斑，此白環與白斑在黑色的頭部均極為醒目，老鳥的枕羽(後頭部)更潔白，所以又叫「白頭翁」。' },
    { id: 2, title: '棲地', text: '白頭翁和麻雀、綠繡眼合稱「城市三寶」，常成群出現在平原區灌木叢、丘陵樹林地帶，以及校園、公園、庭院、行道中的各種高高的電線與樹上。' },
    { id: 3, title: '食性', text: '以果樹的漿果和種子為主食，並時常飛入果園偷吃果實，還會吃嫩葉嫩芽，尤其是胡蝶蘭的嫩葉嫩芽葉，偶爾啄食昆蟲。' }
]
</script>

<style lang="scss" scoped>
.cardList {
    display: flex;
    padding-inline: 55px;
    flex-wrap: wrap;

    .card {
        flex: 1;
        display: flex;
        margin-right: 84px;
        max-width: 278px;
        min-width: 150px;
        margin-right: 2rem;
        text-align: left;
    }

    .cardHeader {
        margin-right: 37px;
        position: relative;
        z-index: 2;
        max-width: 36px;

        //內文標題右下角圓圈設定start
        &::before {
            content: "";
            box-sizing: border-box;
            position: absolute;
            width: 25px;
            height: 25px;
            border-radius: 50%;
            border: 5px solid #AA6666;
            z-index: -1;
            top: 68px;
            right: -12px;
        }

        //內文標題右下角圓圈設定end
        p {
            font-weight: 700;
            font-size: 36px;
            line-height: 40px;
            margin: 0;
        }
    }

    .cardBody {
        font-weight: 400;
        font-size: 16px;
        line-height: 22px;

    }
}

//寬度到一定距離後改為橫向排列，避免內文出現過長的長方形排版，不易閱讀

@media(max-width: 1140px) {
    .cardList {
        flex-direction: column;

        .card {
            padding-top: 50px;
            flex: 1;
            max-width: 100%;
        }
    }
}

@media (max-width: 768px) {
    .cardList {
        padding-inline: 36px;
    }

    .card {
        margin-right: 0;
        max-width: 100%;
    }
}
</style>