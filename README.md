# Web-Form-
<!DOCTYPE html>
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->
<html lang="en">
<head>
<title>Bootstrap Example</title>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="stylesheet"
href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
<script
src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script
src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
</head>
<body>
<div class="container">
<h2>Vertical (basic) form</h2>
<form id="StudentEnrollmentForm" method="post">
<div class="form-group">
<span><label for="rollNo">Roll No:</label> <label id="rollNomsg">
</label></span>
<input type="text" class="form-control" name="Roll No" id="rollNo"
placeholder="Enter Roll No" required>
</div>
<div class="form-group">
<label for="FullName">Full Name:</label>
<input type="text" class="form-control" id="FullName"
placeholder="Enter Full Name" name="FullName">
</div>
<div class="form-group">
<label for="stdClass">Class:</label>
<input type="text" class="form-control" id="stdClass"
placeholder="Enter Class" name="stdClass">
</div>
<div class="form-group">
<label for="Birthdate">Birthdate:</label>
<input type="number" class="form-control" id="Birthdate"
placeholder="Enter Birthdate" name="Birthdate">
</div>
<div class="form-group">
<label for="stdAddress">Address:</label>
<input type="text" class="form-control" id="stdAddress"
placeholder="Enter Address" name="stdAddress">
</div>
<div class="form-group">
<label for="EnrollmentDate">Enrollment Date:</label>
<input type="number" class="form-control" id="EnrollmentDate"
placeholder="Enter Date od Enrollment" name="stdEnrollment Date">
</div>
<input type="button" class="btn btn-primary" id="empSave" value="Save"
onclick="saveEmployee();">
</form>
</div>
<script>
$("#RollNo").focus();
function validateAndGetFormData() {
var RollNoVar = $("#RollNo").val();
if (RollNoVar === "") {
alert("Roll No Required Value");
$("#RollNo").focus();
return "";
}
var FullNameVar = $("#FullName").val();
if (FullNameVar === "") {
alert("Full Name is Required Value");
$("#FullName").focus();
return "";
}
var stdClassVar = $("#stdClass").val();
if (stdClassVar === "") {
alert("Class is Required Value");
$("#stdClass").focus();
return "";
}
var BirthdateVar = $("#Birthdate").val();
if (BirthdateVar === "") {
alert("Birthdate is Required Value");
$("#Birthdate").focus();
return "";
}
var AddressVar = $("#Address").val();
if (AddressVar === "") {
alert("Address is Required Value");
$("#Address").focus();
return "";
}
var EnrollmentDateVar = $("#EnrollmentDate").val();
if (EnrollmentDateVar === "") {
alert("Date on Enrollment is Required Value");
$("#EnrollmentDate").focus();
return "";
}
var jsonStrObj = {
RollNo: RollNoVar,
FullName: FullNameVar,
stdClass: stdClassVar,
Birthdate: BirthdateVar,
Address: AddressVar,
EnrollmentDate: EnrollmentDateVar,
};
return JSON.stringify(jsonStrObj);
}
// This method is used to create PUT Json request.
function createPUTRequest(connToken, jsonObj, dbName, relName) {
var putRequest = "{\n"
+ "\"token\" : \""
+ connToken
+ "\","
+ "\"dbName\": \""
+ dbName
+ "\",\n" + "\"cmd\" : \"PUT\",\n"
+ "\"rel\" : \""
+ relName + "\","
+ "\"jsonStr\": \n"
+ jsonObj
+ "\n"
+ "}";
return putRequest;
}
function executeCommand(reqString, dbBaseUrl, apiEndPointUrl) {
var url = dbBaseUrl + apiEndPointUrl;
var jsonObj;
$.post(url, reqString, function (result) {
jsonObj = JSON.parse(result);
}).fail(function (result) {
var dataJsonObj = result.responseText;
jsonObj = JSON.parse(dataJsonObj);
});
return jsonObj;
}
function resetForm() {
$("#empId").val("")
$("#empName").val("");
$("#empEmail").val("");
$("#empId").focus();
}
function saveEmployee() {
    
    var jsonStr = validateAndGetFormData();
if (jsonStr === "") {
return;
}
var putReqStr = createPUTRequest("90936861|-31948784479254024|90932362",
jsonStr, "SAMPLE", "EMP-REL");
alert(putReqStr);
jQuery.ajaxSetup({async: false});
var resultObj = executeCommand(putReqStr,
"http://api.login2explore.com:5577", "/api/iml");
alert(JSON.stringify(resultObj));
jQuery.ajaxSetup({async: true});
resetForm();
}
</script>
</body>
</html>
