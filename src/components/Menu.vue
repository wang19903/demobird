<template>
    <aside class="menu">
        <input type="checkbox" id="burgerToggle" v-model="isChecked">
        <div class="menuHeader">
            <label for="burgerToggle">
                <div class="burgerBtnContainer">
                    <div class="burgerBtn" ref="burgerBtn"></div>
                </div>
            </label>

            <div class="h2wrap">
                <h2>白頭翁不吃小米</h2>
            </div>
            <div class="logoContainer">
                <div class="logoOutline" />

            </div>
        </div>
        <ul>
            <li :class="{ selected: item.id === selected }" v-for="item in items" :key="item.id" @click="select(item.id)">{{
                item.title }}</li>
        </ul>
    </aside>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
const isChecked = ref<boolean>(false)
const selected = ref<number>(0)
const burgerBtn = ref<HTMLDivElement | null>(null)
//item數量較少沒有跟lists切成兩個componet
const items: { id: number, title: string }[] = [
    { id: 1, title: '白頭翁的特性' },
    { id: 2, title: '白頭翁的故事' },
    { id: 3, title: '白頭翁的美照' },
    { id: 4, title: '白頭翁的危機' }
]
//觸發class渲染條件:click後比對id
const select = (id: number) => {
    selected.value = id
}
//觀察漢堡按鈕，給予class名稱:checked 觸發不同動畫
watch(isChecked, (newVal) => {
    if (burgerBtn.value) {
        burgerBtn.value.classList.toggle('checked', newVal)
    }
});


</script>

<style lang="scss" scoped>
.menu {
    max-width: 345px;
    background: #FFF;
    text-align: center;
    flex: 1;

    .menuHeader {
        display: flex;
        padding-top: 2rem;
        justify-content: center;

    }

    .h2wrap {
        transform: translateX(50px);
    }

    h2 {
        font-weight: 700;
        font-size: 2rem;
        line-height: 41px;
        white-space: nowrap;
    }

    //LOGO圖案start
    .logoContainer {
        box-sizing: border-box;
        width: 91px;
        height: 91px;
        border: gray 1px solid;
        border-radius: 50px;
        right: 0;
        top: 0;
        z-index: 1;
        background: #fff;
        transform: translateX(65px);

        &::after {
            content: "";
            box-sizing: border-box;
            width: 4px;
            height: 4px;
            position: absolute;
            border-radius: 50%;
            border: #000 5px solid;
            right: 30px;
            top: 40px;
        }
    }

    .logoOutline {
        box-sizing: border-box;
        width: 50px;
        height: 60px;
        position: absolute;
        border-radius: 60% 40% 0% 0% / 45% 20%;
        border-top: 8px solid #000;
        top: 22px;
        right: 20px;

        &:before {
            content: "";
            box-sizing: border-box;
            width: 50px;
            height: 60px;
            border-bottom: #000 8px solid;
            border-radius: 0% 0% 45% 0% / 30% 0%;
            position: absolute;
            right: 0px;
            top: -25px;
        }

        &:after {
            content: "";
            box-sizing: border-box;
            width: 15px;
            height: 30px;
            border-radius: 0% 100% 0% 0% / 0% 25%;
            border-top: 8px solid #000;
            position: absolute;
            transform: rotate(-10deg);
            right: -17px;
            top: 4px;
        }
    }

    //LOGO圖案end
    ul {
        padding: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    li {
        font-weight: 400;
        font-size: 18px;
        line-height: 25px;
        padding-top: 17px;
        display: inline-block;
        position: relative;
        user-select: none;
        transition: background-color 0.2s ease-in-out;

        &:hover {
            text-decoration: none; // 讓預設的底線不要出現
            color: #AA6666;
            cursor: pointer;
        }

        &:hover::after {
            content: '';
            position: absolute;
            bottom: 0px; // 控制底線的位置
            left: 0;
            width: 100%;
            height: 1px;
            background-color: #AA6666;
        }

        &:active {
            transform: scale(.95);
        }


    }

    .selected {
        background-color: #DCCCBC;
        border-radius: 10px;
    }

    //漢堡選單桌面板隱藏start
    .burgerBtnContainer {
        display: none;
    }

    #burgerToggle {
        display: none;
    }

    //漢堡選單桌面板隱藏end
}

@media (max-width: 768px) {
    .menu {
        max-width: 100%;
        flex: 0;
        border-bottom: 2px solid rgba(105, 105, 105, .5);
        box-sizing: border-box;

        //漢堡選單設定start
        .burgerBtnContainer {
            display: block;
            width: 35px;
            height: 30px;
            margin: 0 auto;
            margin-top: 2rem;
            cursor: pointer;

            .burgerBtn {
                position: relative;
                height: 5px;
                background: #000;
                width: 30px;

                &:after {
                    //漢堡選單短的橫槓
                    content: "";
                    position: absolute;
                    height: 5px;
                    background: #000;
                    width: 23px;
                    top: 10px;
                    left: 0;
                }

                &::before {
                    content: "";
                    position: absolute;
                    height: 5px;
                    background: #000;
                    width: 30px;
                    top: 20px;
                    left: 0;
                }
            }

            //漢堡選單三橫槓圖案，使用動畫倒放與時間創造hover波浪效果
            &:hover .burgerBtn:not(.checked) {
                animation: wave .8s infinite ease;
            }

            &:hover {
                transform: translateY(10px);

                .burgerBtn {
                    animation: rotate .75s infinite ease;

                }
            }

            &:hover .burgerBtn:not(.checked):before {
                animation: wave .8s infinite ease;
                animation-direction: reverse;
            }

            &:hover .burgerBtn:not(.checked):after {
                //漢堡選單短的橫槓
                animation: waveSmall .7s infinite ease;
                animation-delay: .1s;
            }

            @keyframes rotate {
                0% {
                    transform: rotate(0deg)
                }

                50% {
                    transform: rotate(180deg)
                }

                100% {
                    transform: rotate(360deg)
                }
            }

            @keyframes wave {
                0% {
                    width: 10px;
                }

                50% {
                    width: 30px;
                }

                100% {
                    width: 10px;
                }
            }

            @keyframes waveSmall {

                //漢堡選單短的橫槓波浪效果
                0% {
                    width: 3px;
                }

                50% {
                    width: 23px;
                }

                100% {
                    width: 3px;
                }
            }
        }

        //漢堡選單開關
        #burgerToggle {
            &:checked {
                ~ul {
                    display: flex;
                    opacity: 1;
                    height: 185px;
                }
            }
        }

        //漢堡選單X圖案
        .burgerBtn {
            &.checked {
                transform: rotate(45deg) translateX(20px);

                &:after {
                    transform: rotate(90deg) translate(-15px, -4px);
                }

                &:before {
                    transform: rotate(90deg) translate(-20px, -0.5px);
                }

            }
        }

        //漢堡選單設定end

        .menuHeader {
            justify-content: space-around;
            padding-top: 0;
        }

        .h2wrap {
            transform: translateX(20px);
        }

        h2 {
            font-size: 20px;
            padding-top: 10px;
        }

        .logoContainer {
            transform: scale(.5) translateX(65px);
        }

        ul {
            opacity: 0;
            height: 0;
            margin: 0;
            transition: height 0.5s ease;
        }
    }




}
</style>