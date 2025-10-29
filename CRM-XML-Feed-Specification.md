# Qatar Living CRM XML Feed Specification

## Overview

This document describes the XML feed format required for integrating property listings with Qatar Living's CRM system.

## Feed URL Requirements

- Your XML feed must be accessible via HTTPS
- The feed should return `Content-Type: application/xml`
- The feed must be updated regularly (recommended: real-time or at least hourly)
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

## Complete Example

See `crm-xml-feed-template.xml` for a complete working example.

## Feed Validation

Before going live:

1. **Validate XML syntax** - Ensure your XML is well-formed
2. **Test required fields** - All properties must have required fields
3. **Verify URLs** - All image and photo URLs must be accessible
4. **Check coordinates** - Ensure geopoints are within Qatar (if applicable)

## Processing Notes

- The system processes feeds automatically every day
- Properties not in the feed will be marked as deleted
- Updates are detected via `last_update` timestamp or image changes
- Properties are matched by `reference_number`
- New properties are automatically created
- Existing properties are updated if modified

## Support

For integration support or questions, please contact Technical Support team from Qatar Living website.

---

**Version:** 1.0  
**Last Updated:** Oct 2025
