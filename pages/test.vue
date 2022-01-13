<template>
  <div>
    <v-app id="inspire">
      <v-main>
        <v-card>
          <v-responsive :aspect-ratio="16 / 9">
          <br>
          <v-row>

            <v-col class="col-4 ">
              <v-img
              
                height="300"
                contain
                src="img/25.png"
              ></v-img>
            </v-col>
            <v-col class="col-8"> 
                <div class="triangle-up "></div>
                <div id="container"></div>
            </v-col>
          </v-row>
          </v-responsive>
        </v-card>
      </v-main>
    </v-app>
  </div>
</template>

<script>
anychart.onDocumentReady(function () {

    $('#container').append('<div class="table">' +
        '<table id="table" style="display:none">' +
        '<tr>' +
        '    <td>20</td>' +
        '</tr>' +
        '<tr>' +
        '    <td>7</td>' +
        '</tr>' +
        '<tr>' +
        '    <td>10</td>' +
        '</tr>' +
        '<tr>' +
        '    <td>14</td>' +
        '</tr>' +
        '</table>' +
        '</div>');

    // To work with the data you need to connect data adapter file from https://cdn.anychart.com/

    var tableData = anychart.data.parseHtmlTable('#table');

    var chart = anychart.pyramid();

    // Set data.
    chart.data(tableData);

    chart.title('Set chart data as a table data');
    chart.container('container');
    chart.draw();
});
export default {
  name: "test",
};
</script>
<style scoped>
.triangle-up {
	width: 0;
	height: 0;
	border-left: 25px solid transparent;
	border-right: 25px solid transparent;
	border-bottom: 50px solid #555;
}
html, body, #container {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
}
</style>
