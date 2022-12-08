# BALDongleLib Documentation

## Requirements
Gradle version gradle 7.3.3 and higher.

## The BALLiberies will have multiple aar files, to use the lib download it and place these in your project dependency.
You can achieve this in following ways:-
1. add all the aar files in your project Libs or as a module by impoting it into project in Android studio.
2. add the jitpack dependency like refer [jitpack](https://github.com/nkjha700011/repoD)

## Usage
The below sample of code is in Java syntex may vary in other then java like kotlin or typescript as per platform and language but steps will be same as below.

# Step 1. create the BALBTDongleLib class instance like below
	BALBTDongleLib balBTDongleLib = new BALBTDongleLib(mInputStream,mOutputStream);
	# these parameter are
  
	@NonNull InputStream mInputStream, 
	@NonNull OutputStream mOutputStream 
	which app need to get form 'BluetoothSocket' instance of connected device.

# Step 2. once you have the instance of BALBTDongleLib then you need to initialize the dongle by calling the below function:-
	boolean BTDongleComm = balBTDongleLib.initBTDongleComm(bt_dongle_name);

# List of all the methods along with implementaion details are given below

## Method 1: to read a vin and return live data string, call the below function
	LiveData<String> liveReadVinData = balBTDongleLib.readVIN();

## Method 2: to read VIN in form of a string, call the below function
	String VIN = balBTDongleLib.readVin();

## Method 3: to validate if VIN is not Null and the length of vin is 17, call the below function
	boolean isvalid = balBTDongleLib.isValidVin(vin);
	# the parameter are: @NonNull String vin

## Method 4: to write a vin, call the below function
	balBTDongleLib.writeVIN("MD2B37AXXLPM33903");
	# this parameter is : @NonNull String vin

## Method 5: to get a particular ECU record, call the function below
	ECURecord ecuRecord = balBTDongleLib.getEcuRecord(pos);
	# the parameter is : int pos (position of the a particular record)

## Method 6: to get all the ECU records, call the funtion below
	ArrayList<ECURecord> ecuRecordList= balBTDongleLib.getEcuRecords(ecuRecordsJson);
	# the parameter is : @NonNull String ecuRecordsJson

## Method 7: to get DID groups, call the function below
	ArrayList<String> didGroups = balBTDongleLib.getDIDGroups(ecuRecord);
	# the parameter is: ECURecord ecuRecord

## Method 8: to get the list of DID read parameter names, call the function below
	LiveData<String> readParameterList = balBTDongleLib.getListOfReadParameter(ecuRecord,groupName);
	# the parameter is: ECURecord ecuRecord, String groupName

## Method 9: to get the list of all the error codes, call the function below
	ArrayList errorCodeList = balBTDongleLib.getListOfErrorCode(ecuRecord);
	# the parameter is: ECURecord ecuRecord

## Method 10: to clear the active and inactive error codes, call the function below
	 LiveData<String> clrErrCode= balBTDongleLib.clearErrorCode(ecuRecord);	
	 # the parameter is: ECURecord ecuRecord

## Method 11: to update the status of cleared active and inactive error codes, call the function below
	LiveData<String> clearStatus = balBTDongleLib.clearDTCStaus(ecuRecord);
	# the parameter is: ECURecord ecuRecord

## Method 12: to start the actuator routines, call the function below
	LiveData<String> srtActuRoutines = balBTDongleLib.startActuatorRoutines();

## Method 13: to start the analytics graph, call the function below
	LiveData<String> srtAnaGraph = balBTDongleLib.startAnalyticsGraph();

## Method 14: to update the bootloader, call the function below
	LiveData<String> updateBoot = balBTDongleLib.updateBootLoader();
	
## Method 15: to reset Dongle for other functionality, call the below function 
	balBTDongleLib.resetConfig();

## Method 16: to stop the communication between dongle and application, call the below function
  	readDongleData.stop();

# Implementation Example

```
public class BALBTDongleApiImpl implements BALBTDongleApiLinkage {

    BALBTDongleLib balBTDongleLib;

    public BALBTDongleApiImpl(InputStream mInputStream, OutputStream mOutputStream)  {
        try {
            balBTDongleLib=new BALBTDongleLib(mInputStream,mOutputStream);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    @Override
    public boolean initBTDongleComm(String bt_dongle_name) {
        boolean BTDongleComm=balBTDongleLib.initBTDongleComm(bt_dongle_name);
        return BTDongleComm;
    }

    @Override
    public LiveData<String> readVIN() {
        LiveData<String> liveReadVinData = balBTDongleLib.readVIN();
        return liveReadVinData;
    }

    @Override
    public String readVin() {
        String VIN = balBTDongleLib.readVin();
        return VIN;
    }

    @Override
    public boolean isValidVin(@NonNull String vin) {
        boolean isvalid = balBTDongleLib.isValidVin(vin);
        return isvalid;
    }

    @Override
    public void writeVIN(String vin) {
        balBTDongleLib.writeVIN(vin);
    }

    @Override
    public ArrayList<ECURecord> getEcuRecords(@NonNull String ecuRecordsJson) {
        ArrayList<ECURecord> ecuRecordList= balBTDongleLib.getEcuRecords(ecuRecordsJson);
        return ecuRecordList;
    }

    @Override
    public ECURecord getEcuRecord(int pos) {
        ECURecord ecuRecord = balBTDongleLib.getEcuRecord(pos);
        return ecuRecord;
    }

    @Override
    public ArrayList<String> getDIDGroups(ECURecord ecuRecord) {
        ArrayList<String> didGroups = balBTDongleLib.getDIDGroups(ecuRecord);
        return didGroups;
    }

    @Override
    public LiveData<String> getListOfReadParameter(ECURecord ecuRecord, String groupName) {
        LiveData<String> readParameterList = balBTDongleLib.getListOfReadParameter(ecuRecord,groupName);
        return readParameterList;
    }

    @Override
    public ArrayList getListOfErrorCode(ECURecord ecuRecord) {
        ArrayList errorCodeList = balBTDongleLib.getListOfErrorCode(ecuRecord);
        return errorCodeList;
    }

    @Override
    public LiveData<String> clearErrorCode(ECURecord ecuRecord) {
        LiveData<String> clrErrCode= balBTDongleLib.clearErrorCode(ecuRecord);
        return clrErrCode;
    }

    @Override
    public LiveData<String> clearDTCStaus(ECURecord ecuRecord) {
        LiveData<String> status=balBTDongleLib.clearDTCStaus(ecuRecord);
        return status;
    }

    @Override
    public LiveData<String> startAnalyticsGraph() {
        LiveData<String> srtAnaGraph = balBTDongleLib.startAnalyticsGraph();
        return srtAnaGraph;
    }

    @Override
    public LiveData<String> startActuatorRoutines() {
        LiveData<String> srtActuRoutines = balBTDongleLib.startActuatorRoutines();
        return srtActuRoutines;
    }

    @Override
    public LiveData<String> updateBootLoader() {
        LiveData<String> updateBoot = balBTDongleLib.updateBootLoader();
        return updateBoot;
    }

    @Override
    public void resetConfig() {
        balBTDongleLib.resetConfig();
    }

    @Override
    public void stop() {
        balBTDongleLib.stop();
    }
}

```
