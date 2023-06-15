# currencyConverter


import java.text.DecimalFormat;
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;


public class CurrencyConverter {
    private Map<String, Double> exchangeRates;

    public CurrencyConverter() {
        exchangeRates = new HashMap<>();
        // Set the exchange rates
        exchangeRates.put("USD", 1.0);
        exchangeRates.put("EUR", 0.85);
        exchangeRates.put("GBP", 0.72);
        exchangeRates.put("JPY", 110.26);
        exchangeRates.put("INR", 74.99); // 1 USD = 74.99 INR (example rate)
    }

    public double convert(double amount, String fromCurrency, String toCurrency) {
        if (!exchangeRates.containsKey(fromCurrency) || !exchangeRates.containsKey(toCurrency)) {
            throw new IllegalArgumentException("Invalid currency");
        }

        double fromRate = exchangeRates.get(fromCurrency);
        double toRate = exchangeRates.get(toCurrency);

        double convertedAmount = amount * (toRate / fromRate);
        return convertedAmount;
    }

    public static void main(String[] args) {
        CurrencyConverter converter = new CurrencyConverter();
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the amount to convert: ");
        double amount = scanner.nextDouble();
        scanner.nextLine();

        System.out.print("Enter the currency to convert from (e.g., USD, EUR, GBP, JPY, INR): ");
        String fromCurrency = scanner.nextLine().toUpperCase();

        System.out.print("Enter the currency to convert to (e.g., USD, EUR, GBP, JPY, INR): ");
        String toCurrency = scanner.nextLine().toUpperCase();

        double convertedAmount = converter.convert(amount, fromCurrency, toCurrency);

        DecimalFormat decimalFormat = new DecimalFormat("#,##0.00");
        String formattedAmount = decimalFormat.format(convertedAmount);

        System.out.println("Converted amount: " + formattedAmount + " " + toCurrency);
    }
}
