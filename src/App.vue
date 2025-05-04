<script setup>
import { ref, reactive, nextTick, onMounted, computed } from 'vue';
import { toPng } from 'html-to-image';

const scheduleRef = ref();
function saveImage() {
    toPng(scheduleRef.value).then((dataUrl) => {
        const link = document.createElement('a');
        link.download = 'schedule.png';
        link.href = dataUrl;
        link.click();
    }).catch((err) => {
        console.error('oops, something went wrong!', err);
    });
}

onMounted(() => {
    date.value = monday.value;
    getWeekData(monday.value);
});

const now = ref(new Date());

const getMonday = (date) => {
    const day = date.getDay();
    const diff = date.getDate() - day + (day === 0 ? -6 : 1);
    return new Date(date.setDate(diff)).toISOString().split('T')[0];
};

const monday = computed(() => getMonday(new Date(now.value)));
const date = ref('');
const isView = ref(false);
const dateArray = ref([]);

function getWeekData(dateStr) {
    dateArray.value = [];
    const startDate = new Date(dateStr);
    // 获取一周的日期
    for (let i = 0; i < 7; i++) {
        const currentDate = new Date(startDate);
        currentDate.setDate(startDate.getDate() + i);
        const month = currentDate.getMonth() + 1;
        const day = currentDate.getDate();
        weekData[i].date = `${month}月${day}日`;
        if (i === 0) {
            dateArray.value.push(`${month}月${day}日`);
        }
        if (i === 6) {
            dateArray.value.push(`${month}月${day}日`);
        }
    }
}

const message = reactive([
    {
        title: '任务',
        type: 'success',
        icon: 'List',
        rows: 3,
        desc: '目标接球--观察、摆脱、体位/1v1--距离、节奏、动作/传球-球速、时机、线路。',
    },
    {
        title: '要求',
        type: 'warning',
        icon: 'Histogram',
        rows: 5,
        desc: '行进当中的控制球及瞬间的变化，训练要敢于尝试，只有训练去做了，比赛才可能去做。行进当中的控制球及瞬间的变化，训练要敢于尝试，只有训练去做了，比赛才可能去做。',
    },
    {
        title: '评估',
        type: 'error',
        icon: 'Checked',
        rows: 5,
        desc: '所有技术动作一定是标准，熟练，再加快。很多人只想快，部位不准确。',
    },
]);

const weekData = reactive([
    {
        bgColor: '#409EFF',
        color: '#a0cfff',
        week: '星期一',
        date: '选择日期',
        strength: 3,
        am: {
            status: 'am',
            startTime: '',
            endTime: '',
            position: '',
            items: ["上学"],
            itemValue: '',
            itemVisible: false,
        },
        pm: {
            status: 'pm',
            startTime: '16:00',
            endTime: '18:00',
            position: '超man球场',
            items: ["技术", "传接", "1v1 2v1 2v2", "对抗"],
            itemValue: '',
            itemVisible: false,
        },
    },
    {
        bgColor: '#67C23A',
        color: 'rgb(224.6, 242.8, 215.6)',
        week: '星期二',
        date: '选择日期',
        strength: 5,
        am: {
            status: 'am',
            startTime: '',
            endTime: '',
            position: '',
            items: ["上学"],
            itemValue: '',
            itemVisible: false,
        },
        pm: {
            status: 'pm',
            startTime: '16:00',
            endTime: '18:00',
            position: '超man球场',
            items: ["技术", "传接", "圈抢", "对抗"],
            itemValue: '',
            itemVisible: false,
        },
    },
    {
        bgColor: '#E6A23C',
        color: 'rgb(250, 236.4, 216)',
        week: '星期三',
        date: '选择日期',
        strength: 3,
        am: {
            status: 'am',
            startTime: '',
            endTime: '',
            position: '',
            items: ["上学"],
            itemValue: '',
            itemVisible: false,
        },
        pm: {
            status: 'pm',
            startTime: '15:30',
            endTime: '17:30',
            position: '超man球场',
            items: ["技术", "传接", "1v1 2v1 2v2", "对抗"],
            itemValue: '',
            itemVisible: false,
        },
    },
    {
        bgColor: '#F56C6C',
        color: 'rgb(253, 225.6, 225.6)',
        week: '星期四',
        date: '选择日期',
        strength: 5,
        am: {
            status: 'am',
            startTime: '',
            endTime: '',
            position: '',
            items: ["上学"],
            itemValue: '',
            itemVisible: false,
        },
        pm: {
            status: 'pm',
            startTime: '16:00',
            endTime: '18:00',
            position: '超man球场',
            items: ["技术", "3v1 4v2", "转换", "对抗"],
            itemValue: '',
            itemVisible: false,
        },
    },
    {
        bgColor: '#733ac2',
        color: 'rgb(233 226 253)',
        week: '星期五',
        date: '选择日期',
        strength: 1,
        am: {
            status: 'am',
            startTime: '',
            endTime: '',
            position: '',
            items: ["上学"],
            itemValue: '',
            itemVisible: false,
        },
        pm: {
            status: 'pm',
            startTime: '16:00',
            endTime: '18:00',
            position: '超man球场',
            items: ["技术", "传接", "1v1 2v1 2v2", "战术", "对抗"],
            itemValue: '',
            itemVisible: false,
        },
    },
    {
        bgColor: '#3ac2b5',
        color: '#d8f3ef',
        week: '星期六',
        date: '选择日期',
        strength: 5,
        am: {
            status: 'am',
            startTime: '08:00',
            endTime: '10:00',
            position: '超man球场',
            items: ["大连赢比赛5人制"],
            itemValue: '',
            itemVisible: false,
        },
        pm: {
            status: 'pm',
            startTime: '16:00',
            endTime: '18:00',
            position: '超man球场',
            items: ["小课"],
            itemValue: '',
            itemVisible: false,
        },
    },
    {
        bgColor: '#c23aa9',
        color: 'rgb(243 216 237)',
        week: '星期日',
        date: '选择日期',
        strength: 3,
        am: {
            status: 'am',
            startTime: '08:00',
            endTime: '10:00',
            position: '超man球场',
            items: ["小课"],
            itemValue: '',
            itemVisible: false,
        },
        pm: {
            status: 'pm',
            startTime: '16:00',
            endTime: '18:00',
            position: '超man球场',
            items: ["大连赢比赛5人制"],
            itemValue: '',
            itemVisible: false,
        },
    },
]);

const itemAmRef = new Map();
const itemPmRef = new Map();

const setItemAmRef = (id, el) => {
    if (el) {
        itemAmRef.set(id, el)
    } else {
        itemAmRef.delete(id)
    }
}

const setItemPmRef = (id, el) => {
    if (el) {
        itemPmRef.set(id, el)
    } else {
        itemPmRef.delete(id)
    }
}
const handleClose = (data, tag) => {
    data.items.splice(data.items.indexOf(tag), 1);
}

const showInput = (data, id) => {
    data.itemVisible = true;
    nextTick(() => {
        if (data.status === 'am') {
            itemAmRef.get(id).focus()
        } else {
            itemPmRef.get(id).focus()
        }
    })
}

const handleInputConfirm = (data) => {
    if (data.itemValue) {
        data.items.push(data.itemValue);
    }
    data.itemVisible = false
    data.itemValue = ''
};

const onPreview = () => {
    isView.value = !isView.value;
};

</script>

<template>
    <div class="schedule" :class="{ 'edit': !isView }">
        <div class="schedule-container" ref="scheduleRef">
            <header :class="{ 'edit': !isView }">
                <div class="logo">
                    <el-image style="width: 100px; height: 100px" src="/logo.jpg" fit="cover" />
                </div>
                <h1>谕奇足球俱乐部16、17队周计划<br>{{ dateArray.join(' - ') }}</h1>
            </header>
            <div class="week-message">
                <template v-if="!isView">
                    <div class="edit-item" v-for="item in message" :key="item.title">
                        <h2>{{ item.title }}</h2>
                        <p><el-input v-model="item.desc" :rows="item.rows" type="textarea" placeholder="Please input" clearable /></p>
                    </div>
                </template>
                <template v-else>
                    <el-alert title="如有变化另行通知" type="error" effect="dark" center :closable="false" show-icon>
                        <template #icon>
                            <Bell />
                        </template>
                    </el-alert>
                    <el-alert v-for="item in message" :key="item.title" :closable="false" :title="item.title" :type="item.type" :description="item.desc" show-icon>
                        <template #icon>
                            <component :is="item.icon" />
                        </template>
                    </el-alert>
                </template>
            </div>
            <div class="week-date" v-if="!isView">
                <span>选择周一日期:</span>
                <el-date-picker v-model="date" type="date" placeholder="请选择日期" format="YYYY/MM/DD" value-format="YYYY-MM-DD" @change="getWeekData(date)" />
            </div>
            <ul class="week-list">
                <li class="week-item" v-for="(item, itemIndex) in weekData" :key="item.week" :style="{ '--s-bg-color': item.bgColor, '--s-color': item.color, boxShadow: 'var(--el-box-shadow)' }">
                    <h2 class="week-title">
                        <el-icon>
                            <Calendar />
                        </el-icon>
                        {{ item.week }}
                        <span>({{ item.date }})</span>
                    </h2>
                    <div class="week-rate">
                        <span>训练强度: </span>
                        <el-rate v-model="item.strength" :colors="['#67c23a', '#409eff', '#F56C6C']" />
                    </div>
                    <div class="week-content">
                        <div class="left">
                            <h3>上午</h3>
                            <div class="item-title">
                                <el-icon>
                                    <Timer />
                                </el-icon>
                                时间:
                                <template v-if="isView && item.am.startTime">
                                    {{ item.am.startTime }} - {{ item.am.endTime }}
                                </template>
                            </div>
                            <div class="item-value" v-if="!isView">
                                <el-time-select v-model="item.am.startTime" style="width: 100%" :max-time="item.am.endTime" placeholder="开始时间" start="08:00" step="00:30" end="12:00" />
                                <el-time-select v-model="item.am.endTime" style="width: 100%" :min-time="item.am.startTime" placeholder="结束时间" start="08:00" step="00:30" end="12:00" />
                            </div>
                            <div class="item-title">
                                <el-icon>
                                    <Location />
                                </el-icon>
                                地点:
                                <template v-if="isView">
                                    {{ item.am.position }}
                                </template>
                            </div>
                            <div class="item-value" v-if="!isView">
                                <el-input v-model="item.am.position" style="width: 100%" placeholder="请输入地点" clearable />
                            </div>
                            <div class="item-title">
                                <el-icon>
                                    <Tickets />
                                </el-icon>
                                项目:
                            </div>
                            <div class="item-value">
                                <template v-if="!isView">
                                    <el-tag v-for="(tag, index) in item.am.items" :key="tag + index" closable :disable-transitions="false" @close="handleClose(item.am, tag)"> {{ tag }} </el-tag>
                                    <el-input v-if="item.am.itemVisible" :ref="el => setItemAmRef(itemIndex, el)" v-model="item.am.itemValue" class="w-20" size="small" @keyup.enter="handleInputConfirm(item.am)" @blur="handleInputConfirm(item.am)" />
                                    <el-button v-else class="button-new-tag" size="small" @click="showInput(item.am, itemIndex)"> 新增项目 </el-button>
                                </template>
                                <div class="tag-list" v-if="isView">
                                    <el-tag v-for="(tag, index) in item.am.items" :key="tag + index" effect="dark" :type="(tag === '上学' || tag === '休息') ? 'success' : 'primary'" round size="large">{{ tag }}</el-tag>
                                </div>
                            </div>
                        </div>
                        <div class="right">
                            <h3>下午</h3>
                            <div class="item-title">
                                <el-icon>
                                    <Timer />
                                </el-icon>
                                时间:
                                <template v-if="isView && item.pm.startTime">
                                    {{ item.pm.startTime }} - {{ item.pm.endTime }}
                                </template>
                            </div>
                            <div class="item-value" v-if="!isView">
                                <el-time-select v-model="item.pm.startTime" style="width: 100%" :max-time="item.pm.endTime" placeholder="开始时间" start="12:00" step="00:30" end="20:00" />
                                <el-time-select v-model="item.pm.endTime" style="width: 100%" :min-time="item.pm.startTime" placeholder="结束时间" start="12:00" step="00:30" end="20:00" />
                            </div>
                            <div class="item-title">
                                <el-icon>
                                    <Location />
                                </el-icon>
                                地点:
                                <template v-if="isView">
                                    {{ item.pm.position }}
                                </template>
                            </div>
                            <div class="item-value" v-if="!isView">
                                <el-input v-model="item.pm.position" style="width: 100%" placeholder="请输入地点" clearable />
                            </div>
                            <div class="item-title">
                                <el-icon>
                                    <Tickets />
                                </el-icon>
                                项目:
                            </div>
                            <div class="item-value">
                                <template v-if="!isView">
                                    <el-tag v-for="tag in item.pm.items" :key="tag" closable :disable-transitions="false" @close="handleClose(item.pm, tag)"> {{ tag }} </el-tag>
                                    <el-input v-if="item.pm.itemVisible" :ref="el => setItemPmRef(itemIndex, el)" v-model="item.pm.itemValue" class="w-20" size="small" @keyup.enter="handleInputConfirm(item.pm)" @blur="handleInputConfirm(item.pm)" />
                                    <el-button v-else class="button-new-tag" size="small" @click="showInput(item.pm, itemIndex)"> 新增项目 </el-button>
                                </template>
                                <div class="tag-list" v-if="isView">
                                    <el-tag v-for="(tag, index) in item.pm.items" :key="tag + index" effect="dark" :type="(tag === '上学' || tag === '休息') ? 'success' : 'primary'" round size="large">{{ tag }}</el-tag>
                                </div>
                            </div>
                        </div>
                    </div>
                </li>
            </ul>
        </div>
    </div>

    <footer :class="{ 'edit': !isView }">
        <el-button v-if="!isView" type="success" icon="View" size="large" @click="onPreview">预览</el-button>
        <template v-else>
            <el-button type="primary" icon="Edit" size="large" @click="onPreview">编辑</el-button>
            <el-button type="success" icon="Picture" size="large" @click="saveImage">保存图片</el-button>
        </template>
    </footer>
</template>

<style lang="scss">
.schedule {
    position: relative;
    max-width: 640px;
    width: 640px;
    margin: 0 auto;

    &.edit {
        width: 100%;
    }
}

.schedule-container {
    padding: 15px;
    background-color: #fff;
}

header {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 50px;

    h1 {
        flex: 1;
        text-align: center;
        font-size: 24px;
    }

    &.edit {
        padding: 10px 0;

        h1 {
            font-size: 16px;
        }
    }
}

.week-message {
    .el-alert {
        margin-bottom: 15px;
    }

    .edit-item {
        & + .edit-item {
            margin-top: 15px;
        }
    }
}

.week-date {
    padding: 20px 0;
    display: flex;
    align-items: center;
    gap: 10px;
}

.week-list {

    .week-item {
        margin-top: 15px;
        border: 1px solid var(--s-bg-color);
        border-radius: 10px;
        overflow: hidden;
    }

    .week-title {
        padding: 5px 0;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 10px;
        font-size: 20px;
        font-weight: bold;
        background-color: var(--s-bg-color);
        color: #fff;

        span {
            font-size: 90%;
        }
    }

    .week-rate {
        z-index: 2;
        position: relative;
        padding: 5px 0;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 10px;
        background-color: #fff;

        .el-rate {
            height: 24px;
        }

        .el-rate__item {
            width: 24px;
            height: 24px;
        }

        .el-rate__icon {
            width: 100%;
            height: 100%;

            svg {
                width: 100%;
                height: 100%;
            }
        }
    }

    .week-content {
        display: flex;

        .left,
        .right {
            flex: 0 0 auto;
            width: 50%;
            padding: 10px;
            border-top: 1px solid var(--s-bg-color);
        }

        .left {
            border-right: 1px solid var(--s-bg-color);
        }
    }

    h3 {
        margin: -10px -10px 0 -10px;
        padding: 5px;
        text-align: center;
        background-color: var(--s-color);
        font-weight: bold;
        letter-spacing: 5px;
    }

    .item-title {
        padding: 10px 0 5px;
        display: flex;
        align-items: center;
        gap: 5px;
    }

    .item-value {
        display: flex;
        flex-wrap: wrap;
        gap: 10px;
    }

    .tag-list {
        padding-top: 10px;
        width: 100%;
        height: 100%;
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: center;
        gap: 15px;

        .el-tag__content {
            font-size: 16px;
        }
    }
}

footer {
    max-width: 640px;
    margin: 30px auto 0;
    padding: 15px;

    &.edit {
        text-align: center;
    }
}
</style>
