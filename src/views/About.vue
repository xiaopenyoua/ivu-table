<template>
    <div class="about">
        <Table
            :columns="columns"
            :data="tableData"
            border
            :span-method="arraySpanMethod"
        ></Table>
    </div>
</template>
<script>
export default {
    data() {
        return {
            data: [
                {
                    lxId: "A191001001",
                    contractList: [
                        {
                            id: "A191001001-1",
                            type: "主合同",
                            name: "广粤路074-05地块租赁住宅项目",
                            money: "4,773,000.00",
                            getMoney: "4,773,000.00",
                            notMoney: "4,773,000.00",
                            status: "进行中"
                        },
                        {
                            id: "A191001001-2",
                            type: "主合同",
                            name: "广粤路074-05地块租赁住宅项目",
                            money: "4,773,000.00",
                            getMoney: "4,773,000.00",
                            notMoney: "4,773,000.00",
                            status: "进行中"
                        },
                        {
                            id: "A191001001-3",
                            type: "主合同",
                            name: "广粤路074-05地块租赁住宅项目",
                            money: "4,773,000.00",
                            getMoney: "4,773,000.00",
                            notMoney: "4,773,000.00",
                            status: "进行中"
                        }
                    ]
                },
                {
                    lxId: "A191001002",
                    contractList: [
                        {
                            id: "A191001002-1",
                            type: "主合同",
                            name: "广粤路074-05地块租赁住宅项目",
                            money: "4,773,000.00",
                            getMoney: "4,773,000.00",
                            notMoney: "4,773,000.00",
                            status: "进行中"
                        },
                        {
                            id: "A191001002-2",
                            type: "主合同",
                            name: "广粤路074-05地块租赁住宅项目",
                            money: "4,773,000.00",
                            getMoney: "4,773,000.00",
                            notMoney: "4,773,000.00",
                            status: "进行中"
                        },
                        {
                            id: "A191001002-3",
                            type: "主合同",
                            name: "广粤路074-05地块租赁住宅项目",
                            money: "4,773,000.00",
                            getMoney: "4,773,000.00",
                            notMoney: "4,773,000.00",
                            status: "进行中"
                        },
                        {
                            id: "A191001002-4",
                            type: "主合同",
                            name: "广粤路074-05地块租赁住宅项目",
                            money: "4,773,000.00",
                            getMoney: "4,773,000.00",
                            notMoney: "4,773,000.00",
                            status: "进行中"
                        },
                        {
                            id: "A191001002-5",
                            type: "主合同",
                            name: "广粤路074-05地块租赁住宅项目",
                            money: "4,773,000.00",
                            getMoney: "4,773,000.00",
                            notMoney: "4,773,000.00",
                            status: "进行中"
                        }
                    ]
                }
            ],
            columns: [
                {
                    title: "立项号",
                    key: "lxId"
                },
                {
                    title: "序号",
                    type: "index"
                },
                {
                    title: "合同号",
                    key: "id"
                },
                {
                    title: "合同类型",
                    key: "type"
                },
                {
                    title: "合同名称",
                    key: "name"
                },
                {
                    title: "合同金额",
                    key: "money"
                },
                {
                    title: "合计已收/付款金额",
                    key: "getMoney"
                },
                {
                    title: "合计未收/未付款金额",
                    key: "notMoney"
                },
                {
                    title: "合同状态",
                    key: "status"
                }
            ],
            tableData: []
        };
    },
    methods: {
        // 表格合并方法
        arraySpanMethod({ row, column, rowIndex, columnIndex }) {
            if (columnIndex === 0) {
                if (row.nameIndex) {
                    // 如果有值,说明需要合并
                    return [row.nameIndex, 1];
                } else return [0, 0];
            }
        },

        dealData(data) {
            let getDate = []; // 存储新表格数据
            let nameIndex = [0]; // 保存类型需要合并的值
            data.forEach((v, index) => {
                if (v.contractList.length) {
                    v.contractList.forEach((con, i, conData) => {
                        if (i === conData.length - 1) {
                            nameIndex.push(conData.length);
                        }
                        getDate.push({
                            lxId: v.lxId,
                            id: con.id,
                            type: con.type,
                            name: con.name,
                            money: con.money,
                            getMoney: con.getMoney,
                            notMoney: con.notMoney,
                            status: con.status
                        });
                    });
                }
            });
            console.log(nameIndex, "console.log(nameIndex);");

            let k = 0;
            let t = 0;
            nameIndex.forEach((v, i, nameArr) => {
                console.log(nameArr);
                if (nameArr[i + 1]) {
                    getDate[k].nameIndex = nameArr[i + 1];
                    k += nameArr[i + 1];
                }
            });
            console.log(getDate, "getdata");
            this.tableData = getDate;
        },
        //数字转成货币形式
        numToMoney(num) {
            let numStr = num.toString();
            let str = numStr.split("").reverse();
            for (let i = 0; i < str.length; i++) {
                if ((i + 1) % 4 === 0) {
                    str.splice(i, 0, ",");
                }
            }
            str.reverse();
            let handleResult = "";
            for (let j = 0; j < str.length; j++) {
                handleResult += str[j];
            }
            return handleResult + ".00";
        }
    },
    mounted() {
        this.dealData(this.data);
        // console.log(this.numToMoney("15645156456564844844547484846"));
    }
};
</script>
<style lang="scss" scoped>
.about {
    // width: 960px;
    margin: 0 auto;
}
</style>
