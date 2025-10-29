# Qatar Living CRM Feed - Validation Checklist

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

**Document Version:** 1.0  
**Last Updated:** Oct 2025
