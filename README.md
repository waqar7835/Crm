# Qatar Living CRM Feed Integration Documentation

Welcome to the Qatar Living CRM Property Feed Integration documentation. This guide will help you integrate your property management system with Qatar Living's platform.

## 📚 Documentation Index

### For New Clients

1. **[Quick Start Guide](./CRM-Feed-Quick-Start.md)** ⚡

   - 5-minute setup guide
   - Minimum requirements
   - Common field values
   - Quick examples
   - **Start here if you're new!**

2. **[XML Feed Template](./crm-xml-feed-template.xml)** 📝

   - Ready-to-use XML template
   - Complete example with all fields
   - Multiple property examples
   - Copy and customize for your feed

3. **[Complete Specification](./CRM-XML-Feed-Specification.md)** 📖

   - Detailed field specifications
   - All available options
   - Technical requirements
   - Processing notes
   - **Reference guide for developers**

4. **[Validation Checklist](./CRM-Feed-Validation-Checklist.md)** ✅
   - Pre-integration checklist
   - Quality assurance steps
   - Testing procedures
   - Sign-off document

---

## 🚀 Integration Steps

### Step 1: Understand the Format

Read the **Quick Start Guide** to understand the basic XML structure and required fields.

### Step 2: Create Your Feed

Use the **XML Feed Template** as a starting point. Customize it with your property data.

### Step 3: Validate Your Feed

Use the **Validation Checklist** to ensure your feed meets all requirements.

### Step 4: Reference Details

Consult the **Complete Specification** for detailed information about specific fields.

### Step 5: Submit for Integration

Contact the Qatar Living integration team with your validated feed URL.

---

## 📋 Quick Reference

### Minimum Required Fields

```xml
<property last_update="TIMESTAMP">
  <reference_number>UNIQUE-ID</reference_number>
  <property_type>apartment|villa|office|etc</property_type>
  <offering_type>rent|sale|commercial_rent|commercial_sale</offering_type>
  <title_en>Property Title</title_en>
  <description_en>Property Description</description_en>
  <agent>
    <name>Agent Name</name>
    <email>agent@example.com</email>
    <phone>+974 5555 1234</phone>
  </agent>
</property>
```

### Recommended Fields

- `bedroom`, `bathroom` - Property layout
- `price` - Property price
- `community` - Location
- `photo` - Property images (min 3)
- `geopoints` - Coordinates
- `size` - Built-up area

---

## 🔧 Technical Requirements

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

## 📊 Property Types & Options

### Property Types

**Residential:** apartment, villa, townhouse, studio, penthouse, compound, duplex  
**Commercial:** office, shop, warehouse, showroom, building  
**Land:** land, land_residential, land_commercial  
**Other:** labor_camp

### Offering Types

- `rent` - Residential rental
- `sale` - Residential sale
- `commercial_rent` - Commercial rental
- `commercial_sale` - Commercial sale

### Furnishing Status

- `furnished`
- `semi-furnished`
- `unfurnished`

### Completion Status

- `completed`
- `off_plan`
- `under_construction`

---

## 🖼️ Image Guidelines

- **Format:** JPG, PNG, WebP
- **Minimum Resolution:** 800x600 pixels
- **Recommended:** 1920x1080 pixels
- **Max File Size:** 5MB per image
- **Quantity:** At least 3 images recommended
- First image becomes the featured image

---

## 📞 Support

### Before Contacting Support

✅ **Check:**

1. XML is valid (use online validator)
2. All required fields are present
3. Feed URL is accessible
4. Images load successfully
5. Phone numbers include country code

### Contact Information

- **Technical Support:** [Contact Qatar Living Integration Team]
- **Documentation Issues:** Report via your account manager

---

## 🔄 Feed Processing

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

## ⚠️ Common Issues & Solutions

### Issue: Properties not appearing

**Check:**

- Feed URL is accessible
- XML is well-formed
- All required fields present
- Reference numbers are unique

### Issue: Images not loading

**Check:**

- Image URLs are accessible
- URLs use HTTPS
- Image format is supported
- URLs are properly formatted in XML

### Issue: Agent phone not working

**Check:**

- No spaces or special characters
- Number is valid

### Issue: Location not mapping

**Check:**

- Geopoints format: `latitude,longitude`
- Coordinates are in Qatar range
- Community names are consistent

---

## 📈 Best Practices

### Feed Management

- ✅ Update feed in real-time or daily
- ✅ Use consistent reference numbers
- ✅ Include `last_update` timestamps
- ✅ Validate XML before deploying changes
- ✅ Monitor feed processing logs

### Data Quality

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

**Need help? Contact the Qatar Living Integration Team**

_Last Updated: Oct 2025_
