testi
=====
var SERVER_URL = "http://data.fmi.fi/fmi-apikey/insert-your-apikey-here/wfs";
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
