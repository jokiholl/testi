testi
=====
var SERVER_URL = "http://data.fmi.fi/fmi-apikey/86661e27-1174-4b6f-86aa-e2b3ae46fe54/wfs";
var STORED_QUERY_OBSERVATION = "fmi::observations::weather::multipointcoverage";
var connection = new fi.fmi.metoclient.metolib.WfsConnection();
if (connection.connect(SERVER_URL, STORED_QUERY_OBSERVATION)) {
    // Connection was properly initialized. So, get the data.
    connection.getData({
        requestParameter : "td",
        begin : new Date(1368172800000),
        end : new Date(1368352800000),
        timestep : 60 * 60 * 1000,
        sites : "Helsinki",
        callback : function(data, errors) {
            // Handle the data and errors object in a way you choose.
            handleCallback(data, errors);
            // Disconnect because the flow has finished.
            connection.disconnect();
        }
    });
}
