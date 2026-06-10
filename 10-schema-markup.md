# Schema Markup (JSON-LD)

Schema tells Google what kind of business this is. If you ever get access to add code to the landing page or website, paste these in the `<head>` section.

## ⚠️ Important note

The Iconique landing page is JavaScript-rendered (Next.js). Schema added via JavaScript injection won't be reliably picked up by Google. The clinic's developer needs to add this server-side (in the page's initial HTML).

If you can't get dev access, focus on GBP and citations — schema is a nice-to-have, not a must-have for ranking.

## Schema for the landing page (if dev can add it)

Replace the placeholders before pasting:
- `+63XXXXXXXXX` → real phone formatted as +63 9456675438
- `your-actual-handle` → real social media handles
- `YOUR_GBP_CID` → Google Business Profile CID (find via right-click on GBP card → Copy link)
- Real image URLs

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BeautySalon",
  "@id": "https://www.iconique.com.ph/r/lp/permanent-makeup#business",
  "name": "Reverie Aesthetic and Hair Center",
  "image": [
    "https://www.iconique.com.ph/path-to-logo.jpg",
    "https://www.iconique.com.ph/path-to-storefront.jpg",
    "https://www.iconique.com.ph/path-to-interior.jpg"
  ],
  "logo": "https://www.iconique.com.ph/path-to-logo.jpg",
  "description": "Permanent makeup studio in Salcedo Village, Makati specializing in microblading, eyebrow embroidery, lip blushing, and permanent eyeliner.",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "G/F Office 4, Plaza Royale, L.P. Leviste Street, Salcedo Village",
    "addressLocality": "Makati City",
    "postalCode": "1227",
    "addressRegion": "Metro Manila",
    "addressCountry": "PH"
  },
  "telephone": "+639456675438",
  "email": "booknow.iconique@gmail.com",
  "url": "https://www.iconique.com.ph/r/lp/permanent-makeup",
  "priceRange": "₱₱₱",
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": ["Sunday","Monday","Tuesday","Wednesday","Thursday"],
      "opens": "10:00",
      "closes": "18:00"
    },
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": "Friday",
      "opens": "09:00",
      "closes": "15:00"
    }
  ],
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": "14.5547",
    "longitude": "121.0244"
  },
  "hasMap": "https://maps.google.com/?cid=YOUR_GBP_CID",
  "areaServed": [
    {"@type": "City", "name": "Makati City"},
    {"@type": "City", "name": "Bonifacio Global City"},
    {"@type": "City", "name": "Manila"}
  ],
  "sameAs": [
    "https://www.facebook.com/your-actual-handle",
    "https://www.instagram.com/your-actual-handle",
    "https://www.tiktok.com/@your-actual-handle"
  ],
  "hasOfferCatalog": {
    "@type": "OfferCatalog",
    "name": "Permanent Makeup Services",
    "itemListElement": [
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Microblading"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Eyebrow Embroidery"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Powder Brows"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Ombre Brows"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Lip Blushing"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Lip Tattooing"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Permanent Eyeliner"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Classic Lash Line"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Powder Eyeliner"}},
      {"@type": "Offer", "itemOffered": {"@type": "Service", "name": "Permanent Makeup Touch-ups"}}
    ]
  }
}
</script>
```

## Service-specific schema (advanced, optional)

For individual treatments:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Service",
  "serviceType": "Microblading",
  "name": "Microblading in Makati",
  "description": "Hair-stroke eyebrow tattooing using premium pigments for natural-looking, long-lasting brows.",
  "provider": {
    "@type": "BeautySalon",
    "name": "Reverie Aesthetic and Hair Center",
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "G/F Office 4, Plaza Royale, L.P. Leviste Street, Salcedo Village",
      "addressLocality": "Makati City",
      "postalCode": "1227",
      "addressCountry": "PH"
    }
  },
  "areaServed": "Makati City",
  "offers": {
    "@type": "Offer",
    "price": "14990",
    "priceCurrency": "PHP"
  }
}
</script>
```

## FAQPage schema (if landing page has FAQ section)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "How long does microblading last?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Microblading typically lasts 1-3 years depending on skin type, sun exposure, and aftercare. Touch-ups every 12-18 months keep the color fresh."
      }
    },
    {
      "@type": "Question",
      "name": "Does permanent makeup hurt?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Most clients describe permanent makeup as a mild discomfort, similar to eyebrow threading. A topical numbing cream is applied before the procedure to minimize sensation."
      }
    },
    {
      "@type": "Question",
      "name": "Where is Iconique located?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Our Salcedo Village studio is at G/F Office 4, Plaza Royale, L.P. Leviste Street, Makati City, 1227 Metro Manila. We're open daily 10:00 AM to 9:00 PM."
      }
    }
  ]
}
</script>
```

## How to test schema

After adding to the page, validate at:
- https://validator.schema.org
- https://search.google.com/test/rich-results

Both are free. Paste the URL and they'll show errors or confirm the schema is read correctly.

## If you can't add schema yet

It's fine. Schema is helpful but not required for map pack ranking. Priority order:

1. GBP optimization (file 02) — biggest impact
2. Reviews (file 05) — biggest impact
3. Citations (file 06) — medium impact
4. Schema markup — nice to have

Focus on 1-3 first. Add schema when dev access is possible.
