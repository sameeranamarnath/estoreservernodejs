# estoreservernodejs



<!DOCTYPE html>
<html>
<head>
    <title>Zoho SDK Table Demo</title>
</head>
<body>
    <h1>Table Demo</h1>
    <table id="myTable">
        <thead>
             <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Email</th>
             </tr>
        </thead>
        <tbody>
        </tbody>
    </table>

    <script src="https://www.zohoapis.com/js/sdk/2.0/zoho-sdk.min.js"></script>
    <script>
        ZOHO.initialize({
            client_id: 'YOUR_CLIENT_ID',
            redirect_uri: 'YOUR_REDIRECT_URI',
            scope: 'ZohoCRM.modules.ALL,ZohoCRM.settings.ALL,ZohoCRM.users.ALL',
        });

        ZOHO.CRM.connect().then(function(response) {   
            ZOHO.CRM.API.getRecords({
                module: 'Contacts',
                fields: ['ID', 'Full_Name', 'Email']
            }).then(function(data) {
                var records = data.data;
                var tableBody = '';

                for (var i = 0; i < records.length; i++) {
                    var record = records[i];
                    tableBody += '<tr>';
                    tableBody += '<td>' + record.ID + '</td>';
                    tableBody += '<td>' + record.Full_Name + '</td>';
                    tableBody += '<td>' + record.Email + '</td>';
                    tableBody += '</tr>';
                }

                document.querySelector('#myTable tbody').innerHTML = tableBody;
            });
        });
    </script>
</body>
</html>
