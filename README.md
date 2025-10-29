# Qatar Living CRM Feed Integration - Complete Documentation

**Version:** 1.0  
**Last Updated:** Oct 2025

---

## Table of Contents

1. [Overview & Introduction](#overview--introduction)
2. [Quick Start Guide](#quick-start-guide)
3. [Complete XML Feed Specification](#complete-xml-feed-specification)
4. [Validation Checklist](#validation-checklist)
5. [XML Feed Template](#xml-feed-template)
6. [Common Issues & Solutions](#common-issues--solutions)
7. [Best Practices](#best-practices)
8. [Support](#support)

---

# Overview & Introduction

Welcome to the Qatar Living CRM Property Feed Integration documentation. This comprehensive guide will help you integrate your property management system with Qatar Living's platform.

## 🚀 Integration Steps

### Step 1: Understand the Format

Read the **Quick Start Guide** section to understand the basic XML structure and required fields.

### Step 2: Create Your Feed

Use the **XML Feed Template** section as a starting point. Customize it with your property data.

### Step 3: Validate Your Feed

Use the **Validation Checklist** section to ensure your feed meets all requirements.

### Step 4: Reference Details

Consult the **Complete Specification** section for detailed information about specific fields.

### Step 5: Submit for Integration

Contact the Qatar Living integration team with your validated feed URL.

---

# Quick Start Guide

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

| Residential | Commercial | Land             |
| ----------- | ---------- | ---------------- |
| apartment   | office     | land             |
| villa       | shop       | land_residential |
| townhouse   | warehouse  | land_commercial  |
| studio      | showroom   |                  |
| penthouse   | building   |                  |

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

- **Recommended:** Once a day
- **Minimum:** Daily updates
- System processes feeds automatically every day
- Properties removed from feed will be marked as deleted
- Updates detected via `last_update` timestamp

---

# Complete XML Feed Specification

## Feed URL Requirements

- Your XML feed must be accessible via HTTPS
- The feed should return `Content-Type: application/xml`
- The feed must be updated regularly (recommended: Once a day)
- Feed size should not exceed 50MB for optimal processing

## XML Structure

### Root Element

```xml
<list>
  <property last_update="TIMESTAMP">
    <!-- Property fields here -->
  </property>
</list>
```

## Field Specifications

### Required Fields

| Field              | Type   | Description                          | Example                      |
| ------------------ | ------ | ------------------------------------ | ---------------------------- |
| `reference_number` | String | Unique identifier for the property   | `REF-12345`                  |
| `property_type`    | String | Type of property (see options below) | `apartment`                  |
| `offering_type`    | String | Rent or sale (see options below)     | `rent`                       |
| `title_en`         | String | Property title in English            | `2BR Apartment in The Pearl` |
| `description_en`   | Text   | Detailed description in English      | See template                 |

### Property Type Options

```
Residential:
- apartment
- villa
- townhouse
- studio
- penthouse
- compound
- duplex

Commercial:
- office
- shop
- warehouse
- showroom
- building

Land:
- land
- land_residential
- land_commercial

Other:
- labor_camp
```

### Offering Type Options

```
- rent              (Residential rental)
- sale              (Residential sale)
- commercial_rent   (Commercial rental)
- commercial_sale   (Commercial sale)
```

### Location Fields

| Field           | Required    | Type   | Description               | Example           |
| --------------- | ----------- | ------ | ------------------------- | ----------------- |
| `city`          | Optional    | String | City name                 | `Doha`            |
| `community`     | Recommended | String | Main community/area       | `The Pearl`       |
| `sub_community` | Optional    | String | Sub-area within community | `Porto Arabia`    |
| `geopoints`     | Recommended | String | Coordinates (lat,long)    | `25.3661,51.5242` |

**Note:** Geopoints format is `latitude,longitude` (comma-separated). The system will auto-detect the correct order for Qatar (lat: 24-26, lng: 50-52).

### Property Details

| Field               | Required    | Type    | Description              | Options/Format                               |
| ------------------- | ----------- | ------- | ------------------------ | -------------------------------------------- |
| `bedroom`           | Recommended | Integer | Number of bedrooms       | `0`, `1`, `2`, `3`, `4`, `5`, `6`, `7+`      |
| `bathroom`          | Recommended | Integer | Number of bathrooms      | `1`, `2`, `3`, `4`, `5+`                     |
| `size`              | Recommended | Number  | Built-up area            | Square meters or feet                        |
| `furnished`         | Optional    | String  | Furnishing status        | `furnished`, `semi-furnished`, `unfurnished` |
| `parking`           | Optional    | Integer | Number of parking spaces | `0`, `1`, `2`, `3`, `4+`                     |
| `completion_status` | Optional    | String  | Property status          | `completed`, `off_plan`                      |

### Price Specification

**Option 1: Yearly Rental**

```xml
<price>
  <yearly>120000</yearly>
</price>
```

**Option 2: Monthly Rental**

```xml
<price>
  <monthly>10000</monthly>
</price>
```

**Option 3: Sale Price or Simple Format**

```xml
<price>1500000</price>
```

**Additional Price Fields:**

- `rental_period`: `Y`, `M` (Year, Month)
- `cheques`: Number of cheques (for rental properties)

### Agent Information

| Field         | Required | Type   | Description         | Example             |
| ------------- | -------- | ------ | ------------------- | ------------------- |
| `agent/name`  | Required | String | Agent full name     | `Ahmed Al-Mansoori` |
| `agent/email` | Required | Email  | Agent email address | `ahmed@example.com` |
| `agent/phone` | Required | String | Agent phone         | `+974 5555 1234`    |
| `agent/photo` | Optional | URL    | Agent photo URL     | `https://...`       |

**Phone Number Format:**

- Include country code: `+974` for Qatar
- Remove extra spaces (system will auto-clean)
- Example: `+974 5555 1234` or `+97455551234`

### Images

Images should be provided as multiple URL elements:

```xml
<photo>
  <url _="https://example.com/image1.jpg" />
  <url _="https://example.com/image2.jpg" />
  <url _="https://example.com/image3.jpg" />
</photo>
```

**Image Requirements:**

- Format: JPG, PNG, WebP
- Minimum resolution: 800x600 pixels
- Recommended: 1920x1080 pixels
- Maximum file size: 5MB per image
- At least 3 images recommended

### Amenities/Facilities

Choose ONE of the following formats:

**Option 1: Commercial Amenities** (for commercial properties)

```xml
<commercial_amenities>Conference Room,Parking,24/7 Security,Central AC</commercial_amenities>
```

**Option 2: Private Amenities** (for residential properties)

```xml
<private_amenities>Swimming Pool,Gym,Garden,Balcony,Maid Room</private_amenities>
```

**Option 3: General Amenities**

```xml
<amenities>Swimming Pool,Gym,Kids Play Area,BBQ Area,Security</amenities>
```

**Common Amenities:**

```
Residential:
- Swimming Pool
- Gym
- Garden
- Balcony
- Maid Room
- Driver Room
- Storage Room
- Kids Play Area
- BBQ Area
- Central AC
- 24/7 Security
- Covered Parking
- Laundry Room

Commercial:
- Conference Room
- Reception
- Parking
- Central AC
- 24/7 Security
- Elevator
- Pantry
- Server Room
```

### Last Update Timestamp

```xml
<property last_update="2025-01-15T10:30:00Z">
```

**Format:** ISO 8601 timestamp (UTC recommended)

- Example: `2025-01-15T10:30:00Z`
- Used to detect property updates

## Feed Processing

### How It Works

1. System fetches your XML feed every day
2. Properties are matched by `reference_number`
3. New properties are created automatically
4. Existing properties are updated if modified
5. Properties not in feed are marked as deleted

### Update Detection

Updates are detected via:

- `last_update` timestamp changes
- Image URL changes

---

# Validation Checklist

## ✅ Pre-Integration Checklist

### 1. Feed Accessibility

- [ ] Feed URL is publicly accessible
- [ ] Feed URL uses HTTPS (not HTTP)
- [ ] Feed returns `Content-Type: application/xml` header
- [ ] Feed loads within 30 seconds
- [ ] Feed size is under 50MB

### 2. XML Structure

- [ ] XML has proper declaration: `<?xml version="1.0" encoding="UTF-8"?>`
- [ ] Root element is `<list>`
- [ ] All properties are within `<property>` tags
- [ ] XML is well-formed (no syntax errors)
- [ ] All tags are properly closed

### 3. Required Fields (Per Property)

#### Identification

- [ ] `reference_number` - Unique for each property
- [ ] No duplicate reference numbers in feed

#### Property Classification

- [ ] `property_type` - Valid value from accepted list
- [ ] `offering_type` - Valid value (rent/sale/commercial_rent/commercial_sale)

#### Property Information

- [ ] `title_en` - Descriptive title present
- [ ] `description_en` - Detailed description present
- [ ] Description is readable (not just keywords)

#### Agent Details

- [ ] `agent/name` - Agent name provided
- [ ] `agent/email` - Valid email format
- [ ] `agent/phone` - Includes country code (+974 for Qatar)
- [ ] Phone number is numeric (after country code)

### 4. Recommended Fields

#### Location

- [ ] `community` - Main area/community specified
- [ ] `sub_community` - Sub-area specified (if applicable)
- [ ] `city` - City name provided
- [ ] `geopoints` - Coordinates in format: latitude,longitude
- [ ] Coordinates are valid Qatar locations (lat: 24-26, lng: 50-52)

#### Property Details

- [ ] `bedroom` - Number of bedrooms
- [ ] `bathroom` - Number of bathrooms
- [ ] `size` - Built-up area in sqm or sqft
- [ ] `furnished` - Furnishing status specified
- [ ] `parking` - Number of parking spaces

#### Pricing

- [ ] `price` - Price is provided
- [ ] Price is numeric (no currency symbols or commas)
- [ ] Price structure is correct (yearly/monthly/simple)
- [ ] `rental_period` or `frequency` specified for rentals

#### Media

- [ ] `photo` - At least 1 image URL provided
- [ ] Minimum 3 images recommended
- [ ] All image URLs are accessible
- [ ] Images are valid format (JPG/PNG/WebP)
- [ ] Images load successfully

### 5. Data Quality

#### Reference Numbers

- [ ] All reference numbers are unique within the feed
- [ ] Reference numbers are consistent (same format)
- [ ] Reference numbers don't change for same property

#### Consistency

- [ ] Property types use consistent values
- [ ] Offering types are correctly categorized
- [ ] Price units are consistent across properties
- [ ] Location names are standardized

#### Agent Information

- [ ] Agent emails are valid and deliverable
- [ ] Phone numbers follow consistent format
- [ ] Agent names are properly formatted
- [ ] Agent photos load successfully (if provided)

### 6. Content Quality

#### Titles

- [ ] Titles are descriptive and unique
- [ ] Titles include key property features
- [ ] Titles are in English
- [ ] No all-caps titles
- [ ] No excessive punctuation

#### Descriptions

- [ ] Descriptions are detailed and informative
- [ ] Descriptions are formatted properly
- [ ] No HTML tags in descriptions (or properly formatted)
- [ ] Descriptions highlight key features
- [ ] Contact information not in description (use agent fields)

#### Images

- [ ] First image is main/featured image
- [ ] Images are high quality (min 800x600px)
- [ ] Images show property (not logos/watermarks only)
- [ ] Images are properly oriented
- [ ] Consistent image quality across properties

### 7. Optional Enhancements

- [ ] `amenities` or `private_amenities` - Facilities listed
- [ ] `completion_status` - Property status specified
- [ ] `last_update` - Timestamp attribute on property tag
- [ ] Amenities are relevant to property type

### 8. Technical Validation

#### XML Validation

- [ ] XML validates against standard parsers
- [ ] No special characters breaking XML structure
- [ ] UTF-8 encoding is correct
- [ ] No BOM (Byte Order Mark) issues

#### URL Encoding

- [ ] All URLs are properly encoded
- [ ] Special characters in URLs are escaped
- [ ] Image URLs don't contain spaces

#### Data Types

- [ ] Numbers are in correct format (no text in numeric fields)
- [ ] Dates/timestamps are in ISO 8601 format
- [ ] Boolean values are consistent

### 9. Feed Updates

- [ ] Feed can be refreshed without errors
- [ ] New properties appear in feed
- [ ] Removed properties are excluded from feed
- [ ] Updated properties show new `last_update` timestamp
- [ ] Feed update frequency is documented

## 🔍 Sample Property Test

- [ ] Appears in feed correctly
- [ ] All required fields present
- [ ] Images load successfully
- [ ] Agent contact information correct
- [ ] Location data accurate
- [ ] Price displays correctly

---

## ✅ Final Approval

- [ ] All required fields validated
- [ ] All recommended fields reviewed
- [ ] Data quality meets standards
- [ ] Feed performs adequately
- [ ] Client notified of any issues
- [ ] Feed ready for production

## 🔄 Next Steps

1. [ ] Schedule feed activation
2. [ ] Monitor first sync
3. [ ] Verify properties in CRM
4. [ ] Check property mapping
5. [ ] Confirm with client
6. [ ] Schedule follow-up review

---

# XML Feed Template

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--
  Qatar Living Property Feed Template
  ====================================
  This XML template shows the required format for property feeds.
  Replace example values with your actual property data.
-->
<list>
  <property last_update="2025-01-15T10:30:00Z">

    <!-- REQUIRED FIELDS -->
    <reference_number>REF-12345</reference_number>

    <!-- PROPERTY TYPE -->
    <!-- Options: apartment, villa, townhouse, penthouse, compound, office, shop, warehouse, showroom, labor_camp, land, building, studio, duplex -->
    <property_type>apartment</property_type>

    <!-- AD/OFFERING TYPE -->
    <!-- Options: rent, sale, commercial_rent, commercial_sale -->
    <offering_type>rent</offering_type>

    <!-- PROPERTY DETAILS -->
    <title_en>Luxurious 2 Bedroom Apartment in The Pearl</title_en>
    <description_en>Beautiful and spacious apartment with modern amenities.

Features:
- Open kitchen
- Balcony with sea view
- Gym and pool access
- 24/7 security</description_en>

    <!-- SIZE -->
    <!-- Built-up area in square meters or square feet -->
    <size>120</size>

    <!-- LOCATION -->
    <city>Doha</city>
    <community>The Pearl</community>
    <sub_community>Porto Arabia</sub_community>

    <!-- BEDROOMS & BATHROOMS -->
    <!-- Use numbers: 0, 1, 2, 3, 4, 5, 6, 7+ -->
    <bedroom>2</bedroom>
    <bathroom>2</bathroom>

    <!-- PRICE -->
    <!-- Option 1: Yearly rent -->
    <price>
      <yearly>120000</yearly>
    </price>

    <!-- Option 2: Monthly rent -->
    <!-- <price>
      <monthly>10000</monthly>
    </price> -->

    <!-- Option 3: Sale price or simple price -->
    <!-- <price>1500000</price> -->

    <!-- FREQUENCY/RENTAL PERIOD (if not specified in price) -->
    <!-- Options: Y (yearly), M (monthly), D (daily), W (weekly) -->
    <!-- <rental_period>Y</rental_period> -->

    <!-- CHEQUES (number of cheques for rent) -->
    <!-- <cheques>1</cheques> -->

    <!-- FURNISHING STATUS -->
    <!-- Options: furnished, semi-furnished, unfurnished -->
    <furnished>furnished</furnished>

    <!-- PARKING -->
    <!-- Number of parking spaces -->
    <parking>2</parking>

    <!-- COMPLETION STATUS -->
    <!-- Options: completed, off_plan, under_construction -->
    <completion_status>completed</completion_status>

    <!-- LOCATION COORDINATES -->
    <!-- Format: latitude,longitude -->
    <geopoints>25.3661,51.5242</geopoints>

    <!-- AGENT INFORMATION -->
    <agent>
      <name>Ahmed Al-Mansoori</name>
      <email>ahmed@example.com</email>
      <phone>+974 5555 1234</phone>
      <!-- Agent photo URL (optional) -->
      <photo>https://example.com/agent-photo.jpg</photo>
    </agent>

    <!-- IMAGES -->
    <!-- Multiple image URLs -->
    <photo>
      <url _="https://example.com/property/image1.jpg" />
      <url _="https://example.com/property/image2.jpg" />
      <url _="https://example.com/property/image3.jpg" />
      <url _="https://example.com/property/image4.jpg" />
    </photo>

    <!-- AMENITIES/FACILITIES -->
    <!-- Option 1: Commercial amenities (for commercial properties) -->
    <commercial_amenities>Conference Room,Parking,24/7 Security,Central AC,Reception</commercial_amenities>

    <!-- Option 2: Private amenities (for residential properties) -->
    <!-- <private_amenities>Swimming Pool,Gym,Garden,Balcony,Maid Room,Storage</private_amenities> -->

    <!-- Option 3: General amenities -->
    <!-- <amenities>Swimming Pool,Gym,Kids Play Area,BBQ Area,Security,Covered Parking</amenities> -->

  </property>

  <!-- Add more <property> elements for additional properties -->
  <property last_update="2025-01-15T11:00:00Z">
    <reference_number>REF-12346</reference_number>
    <property_type>villa</property_type>
    <offering_type>sale</offering_type>
    <title_en>Stunning 4BR Villa with Private Pool</title_en>
    <description_en>Spacious family villa in prime location</description_en>
    <size>350</size>
    <city>Doha</city>
    <community>West Bay</community>
    <sub_community>Diplomatic Area</sub_community>
    <bedroom>4</bedroom>
    <bathroom>5</bathroom>
    <price>4500000</price>
    <furnished>unfurnished</furnished>
    <parking>3</parking>
    <completion_status>completed</completion_status>
    <geopoints>25.3200,51.5300</geopoints>
    <agent>
      <name>Sarah Johnson</name>
      <email>sarah@example.com</email>
      <phone>+974 5555 5678</phone>
    </agent>
    <photo>
      <url _="https://example.com/villa/image1.jpg" />
      <url _="https://example.com/villa/image2.jpg" />
    </photo>
    <private_amenities>Swimming Pool,Garden,Maid Room,Driver Room,Laundry Room</private_amenities>
  </property>

</list>
```

---

# Common Issues & Solutions

## Issue: Properties not appearing

**Check:**

- Feed URL is accessible
- XML is well-formed
- All required fields present
- Reference numbers are unique

## Issue: Images not loading

**Check:**

- Image URLs are accessible
- URLs use HTTPS
- Image format is supported
- URLs are properly formatted in XML

## Issue: Agent phone not working

**Check:**

- Phone number includes country code (+974)
- No spaces or special characters
- Number is valid

## Issue: Location not mapping

**Check:**

- Geopoints format: `latitude,longitude`
- Coordinates are in Qatar range
- Community names are consistent

---

# Best Practices

## Feed Management

- ✅ Update feed in real-time or daily
- ✅ Use consistent reference numbers
- ✅ Include `last_update` timestamps
- ✅ Validate XML before deploying changes
- ✅ Monitor feed processing logs

## Data Quality

- ✅ Write descriptive titles and descriptions
- ✅ Include high-quality images
- ✅ Provide accurate location data
- ✅ Keep agent information current
- ✅ Use standardized property types

## 🎯 Getting Started Checklist

- [ ] Read Quick Start Guide
- [ ] Download XML Feed Template
- [ ] Customize template with your data
- [ ] Validate XML structure
- [ ] Test feed URL accessibility
- [ ] Complete Validation Checklist
- [ ] Submit feed URL to Qatar Living
- [ ] Monitor first sync
- [ ] Verify properties in system

---

# Support

## Before Contacting Support

✅ **Check:**

1. XML is valid (use online validator)
2. All required fields are present
3. Feed URL is accessible
4. Images load successfully
5. Phone numbers include country code

## Contact Information

- **Technical Support:** Contact Qatar Living Integration Team via website
- **Documentation Issues:** Report via your account manager

---

## 📊 Technical Requirements Summary

### Feed URL

- Must be publicly accessible
- HTTPS required
- Returns valid XML
- Updates regularly (daily recommended)
- Max size: 50MB

### XML Format

- UTF-8 encoding
- Root element: `<list>`
- Properties in `<property>` tags
- Well-formed XML structure

### Data Quality

- Unique reference numbers
- Valid phone numbers with country code
- Accessible image URLs
- Accurate coordinates (for Qatar: lat 24-26, lng 50-52)
- Numeric prices (no symbols)

---

**Need help? Contact the Qatar Living Integration Team**

_Last Updated: Oct 2025_
