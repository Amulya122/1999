import java.util.HashMap;
import java.util.Map;
import java.util.Random;

public class LinkShortener {

    private static final String CHARACTERS = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    private static final int SHORT_URL_LENGTH = 6;

    private Map<String, String> shortToLongUrlMap;
    private Map<String, String> longToShortUrlMap;
    private Random random;

    public LinkShortener() {
        this.shortToLongUrlMap = new HashMap<>();
        this.longToShortUrlMap = new HashMap<>();
        this.random = new Random();
    }

    public String shortenUrl(String longUrl) {
        if (longToShortUrlMap.containsKey(longUrl)) {
            return longToShortUrlMap.get(longUrl);
        } else {
            String shortUrl = generateShortUrl();
            shortToLongUrlMap.put(shortUrl, longUrl);
            longToShortUrlMap.put(longUrl, shortUrl);
            return shortUrl;
        }
    }

    public String expandUrl(String shortUrl) {
        return shortToLongUrlMap.getOrDefault(shortUrl, "Short URL not found");
    }

    private String generateShortUrl() {
        StringBuilder shortUrl = new StringBuilder();
        for (int i = 0; i < SHORT_URL_LENGTH; i++) {
            int randomIndex = random.nextInt(CHARACTERS.length());
            shortUrl.append(CHARACTERS.charAt(randomIndex));
        }
        return shortUrl.toString();
    }

    public static void main(String[] args) {
        LinkShortener linkShortener = new LinkShortener();

        // Example usage
        String longUrl1 = "https://www.example.com/article/how-to-build-a-link-shortener";
        String shortUrl1 = linkShortener.shortenUrl(longUrl1);
        System.out.println("Shortened URL for " + longUrl1 + ": " + shortUrl1);

        String longUrl2 = "https://www.example.com/about";
        String shortUrl2 = linkShortener.shortenUrl(longUrl2);
        System.out.println("Shortened URL for " + longUrl2 + ": " + shortUrl2);

        String expandedUrl = linkShortener.expandUrl(shortUrl2);
        System.out.println("Expanded URL for " + shortUrl2 + ": " + expandedUrl);
    }
}

