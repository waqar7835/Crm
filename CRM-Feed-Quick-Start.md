# Qatar Living CRM Feed - Quick Start Guide

## 🚀 Getting Started in 5 Minutes

### Step 1: Create Your XML Feed

Your feed must be a publicly accessible URL that returns XML in this format:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<list>
  <property last_update="2025-01-15T10:30:00Z">
    <reference_number>UNIQUE-REF-001</reference_number>
    <property_type>apartment</property_type>
    <offering_type>rent</offering_type>
    <title_en>Your Property Title</title_en>
    <description_en>Your property description</description_en>
    <bedroom>2</bedroom>
    <bathroom>2</bathroom>
    <size>120</size>
    <price><yearly>120000</yearly></price>
    <community>The Pearl</community>
    <agent>
      <name>Agent Name</name>
      <email>agent@example.com</email>
      <phone>+974 5555 1234</phone>
    </agent>
    <photo>
      <url _="https://example.com/image1.jpg" />
    </photo>
  </property>
</list>
```

### Step 2: Minimum Required Fields

✅ **Must Have:**
- `reference_number` - Unique ID for each property
- `property_type` - apartment, villa, office, etc.
- `offering_type` - rent, sale, commercial_rent, commercial_sale
- `title_en` - Property title
- `description_en` - Property description
- `agent/name` - Agent name
- `agent/email` - Agent email
- `agent/phone` - Agent phone with country code

### Step 3: Recommended Fields for Better Listings

⭐ **Highly Recommended:**
- `bedroom` - Number of bedrooms
- `bathroom` - Number of bathrooms
- `price` - Property price
- `community` - Location area
- `photo` - At least 3 property images
- `geopoints` - Latitude,Longitude coordinates
- `size` - Built-up area

### Step 4: Common Field Values

#### Property Types
| Residential | Commercial | Land |
|------------|------------|------|
| apartment | office | land |
| villa | shop | land_residential |
| townhouse | warehouse | land_commercial |
| studio | showroom | |
| penthouse | building | |

#### Offering Types
- `rent` - Residential rent
- `sale` - Residential sale
- `commercial_rent` - Commercial rent
- `commercial_sale` - Commercial sale

#### Furnishing Status
- `furnished`
- `semi-furnished`
- `unfurnished`

#### Price Format

**For Rent (Yearly):**
```xml
<price><yearly>120000</yearly></price>
```

**For Rent (Monthly):**
```xml
<price><monthly>10000</monthly></price>
```

**For Sale:**
```xml
<price>1500000</price>
```

### Step 5: Testing Your Feed

**Checklist:**
- [ ] Feed URL is accessible via HTTPS
- [ ] XML is valid (use online XML validator)
- [ ] All properties have unique `reference_number`
- [ ] Agent phone numbers include country code (+974)
- [ ] All image URLs are accessible
- [ ] Price values are numeric (no currency symbols)
- [ ] `last_update` timestamp is in ISO format

### Step 6: Feed Submission

Once your feed is ready:
1. Test the feed URL in a browser
2. Verify all required fields are present
3. Provide the feed URL to Qatar Living team
4. Wait for feed activation (usually 24-48 hours)

---

## 📋 Field Mapping Examples

### Location Fields
```xml
<city>Doha</city>
<community>The Pearl</community>
<sub_community>Porto Arabia</sub_community>
<geopoints>25.3661,51.5242</geopoints>
```

### Agent Information
```xml
<agent>
  <name>Ahmed Al-Mansoori</name>
  <email>ahmed@realestate.com</email>
  <phone>+974 5555 1234</phone>
  <photo>https://example.com/agent.jpg</photo>
</agent>
```

### Property Images
```xml
<photo>
  <url _="https://example.com/bedroom.jpg" />
  <url _="https://example.com/kitchen.jpg" />
  <url _="https://example.com/bathroom.jpg" />
  <url _="https://example.com/living-room.jpg" />
</photo>
```

### Amenities
```xml
<!-- Comma-separated list -->
<private_amenities>Swimming Pool,Gym,Garden,Balcony,Maid Room,24/7 Security</private_amenities>
```

---

## ⚠️ Common Mistakes to Avoid

### ❌ Don't:
```xml
<!-- Missing country code -->
<phone>5555 1234</phone>

<!-- Price with currency symbol -->
<price>QAR 120,000</price>

<!-- Invalid XML structure -->
<photo>https://example.com/image.jpg</photo>

<!-- Missing reference number -->
<property>
  <title_en>Nice Apartment</title_en>
</property>
```

### ✅ Do:
```xml
<!-- Include country code -->
<phone>+974 5555 1234</phone>

<!-- Numeric price only -->
<price>120000</price>

<!-- Proper XML structure -->
<photo>
  <url _="https://example.com/image.jpg" />
</photo>

<!-- Always include reference -->
<property>
  <reference_number>PROP-001</reference_number>
  <title_en>Nice Apartment</title_en>
</property>
```

---

## 🔄 Feed Update Frequency

- **Recommended:** Real-time or hourly updates
- **Minimum:** Daily updates
- System processes feeds automatically every hour
- Properties removed from feed will be marked as deleted
- Updates detected via `last_update` timestamp

---

## 📞 Need Help?

**Resources:**
- 📄 **Full Specification:** See `CRM-XML-Feed-Specification.md`
- 📝 **XML Template:** See `crm-xml-feed-template.xml`
- 🔧 **Technical Support:** Contact Qatar Living Integration Team

**Before contacting support, please:**
1. Validate your XML syntax
2. Check all required fields are present
3. Verify your feed URL is accessible
4. Test with at least 2-3 sample properties

---

**Happy Integrating! 🎉**
