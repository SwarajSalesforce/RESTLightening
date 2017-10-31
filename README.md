# RESTLightening Exchange Rate

## Step 1 :  Authorize the endpoint URL For Apex Callout.

 For Authorize the endpoint URL -:

From Setup, enter Remote Site Settings in the Quick Find box

Click on the Remote Site Settings.

Click New Remote Site.

For the remote site name, enter foreign_exchange_rates .

For the remote site URL, enter http://api.fixer.io  ,This URL authorizes all subfolders for the endpoint, like http://api.fixer.io/latest

Make sure your Active checkbox is Equal to True.

Click Save.

## Step 2 :  Create Apex Class For Make HTTP Callouts.

Apex class httpCallOutCtrl.apxc

public class httpCallOutCtrl {
	// Pass in the endpoint to be used using the string url
	@AuraEnabled
	public static Map < String,
	Object > getCalloutResponseContents(String url) {
 
		// Instantiate a new http object
		Http h = new Http();
 
		// Instantiate a new HTTP request, specify the method (GET) as well as the endpoint
		HttpRequest req = new HttpRequest();
		req.setEndpoint(url);
		req.setMethod('GET');
 
		// Send the request, and return a response
		HttpResponse res = h.send(req);
		System.debug('response:--> ' + res.getBody());
 
		// Deserialize the JSON string into collections of primitive data types.
		Map < String,
		Object > resultsMap = (Map < String, Object > ) JSON.deserializeUntyped(res.getBody());
		system.debug('resultsMap-->' + resultsMap);
 
		return resultsMap;
	}
}
