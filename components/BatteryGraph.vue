<template>
    <div>
        <canvas id="myLineChart"></canvas>
    </div>
</template>

<script setup>
import * as dayjs from 'dayjs'
import Chart from 'chart.js/auto';

const props = defineProps({
    BatteryArray: {
        type: Array,
        required: true,
    },
});


//Data manipulation
onMounted(() => {
    const ctxLine = document.getElementById('myLineChart');

    const BatteryLevels = [];
    const BatteryDate = [];

    props.BatteryArray.forEach(element => {
        let tempDate = dayjs(element.timestamp).toDate();

        const TempDateActually = new Date(tempDate);

        var dd = TempDateActually.getDate();
        var mm = TempDateActually.getMonth() + 1;
        var yyyy = TempDateActually.getFullYear();
        if (dd < 10) {
            dd = '0' + dd;
        }

        if (mm < 10) {
            mm = '0' + mm;
        }

        const visualDate = mm + '-' + dd + '-' + yyyy;
        BatteryDate.push(visualDate);
        BatteryLevels.push(element.battery);
    });


    console.log(batteryData);
    //Line chart
    new Chart(ctxLine, {
        type: 'line',
        data: {
            labels: BatteryDate,
            datasets: [{
                label: '% Battery - UNIT: ' + batteryData.chapters[0]['device_udid'] + ' - ' + 'Firmware:' + batteryData.chapters[0]['firmware'],
                data: BatteryLevels,
                borderWidth: 1,
            }]
        },
        options: {
            indexAxis: 'x',
            scales: {
                y: {
                    min: 0,
                    max: 100
                }
            }
        }
    });

});

</script>