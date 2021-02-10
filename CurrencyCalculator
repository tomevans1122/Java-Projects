
import org.json.JSONObject;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.InputMismatchException;
import java.util.Scanner;

public class Money {


    // MAIN EXECUTION SCRIPT

    public static HttpURLConnection connection;

    public static void main(String[] args) {
        BufferedReader reader;
        String line;
        StringBuilder responseContent = new StringBuilder();

        try {
            URL url = new URL ("https://api.exchangeratesapi.io/latest?base=GBP");
            connection = (HttpURLConnection) url.openConnection();

            // request set up
            connection.setRequestMethod("GET");
            connection.setConnectTimeout(5000);
            connection.setReadTimeout(5000);

            int status = connection.getResponseCode();
            //System.out.println(status);
            if (status > 299){
                reader = new BufferedReader(new InputStreamReader(connection.getErrorStream()));
            } else {
                reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));

            }
            while ((line = reader.readLine()) != null){
                responseContent.append(line);
            }
            reader.close();

            JSONObject myresponse = new JSONObject(responseContent.toString());
            //System.out.println(myresponse);
            // for parsing date
            //System.out.println(myresponse.getString("date"));
            // for parsing base
            //System.out.println(myresponse.getString("base"));

            // rates are enclosed, and is an object not auto
            JSONObject ratesObject = new JSONObject(myresponse.getJSONObject("rates").toString());
            //System.out.println(ratesObject);

            // for specific currency
            //System.out.println("USD = $" + ratesObject.getDouble("USD"));

            // CREATE THE QUESTIONS WITHIN THE TRY-CATCH LOOP OF THE API HERE
            // TIDY IT UP LATER
            double val = currencyInput();
            System.out.println("That is £" + val); //Value in £
            System.out.println("Please choose to convert to either EUR or USD: ");
            Scanner input = new Scanner(System.in);
            String chosenCurrency = input.next(); // player chooses EUR or USD currency
            System.out.println(chosenCurrency);
            double convertedVal = val * (ratesObject.getDouble(chosenCurrency));
            if (chosenCurrency.equals("USD")) {
                System.out.println("That is $" + convertedVal);
            } else if (chosenCurrency.equals("EUR")){
                System.out.println("That is €" + convertedVal);
            } else{
                System.out.println("That is not an appropriate choice, run again.");
            }




        } catch (IOException e) {
            e.printStackTrace();
        }


    } // End of main execution script

    // METHOD FOR RECEIVING VALID VALUE INPUT
    public static double currencyInput() {
        Scanner input = new Scanner(System.in);
        while(true){
            try{
                System.out.println("Please input positive value in GBP sterling. " +
                        "If negative value is given you will be asked again:");
                return input.nextDouble();
            } catch (InputMismatchException e){
                String bad_input = input.next();
                System.out.println(bad_input + " is not an appropriate value.");
            }
        }
    }
