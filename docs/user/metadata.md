# Metadata

## Reading metadata

```python
from pypdf import PdfReader

reader = PdfReader("example.pdf")

meta = reader.metadata

print(len(reader.pages))

# All of the following could be None!
print(meta.author)
print(meta.creator)
print(meta.producer)
print(meta.subject)
print(meta.title)
```

## Writing metadata

```python
from datetime import datetime
from pypdf import PdfReader, PdfWriter

reader = PdfReader("example.pdf")
writer = PdfWriter()

# Add all pages to the writer
for page in reader.pages:
    writer.add_page(page)

# # If you want to add the old metadata, include this line
metadata = reader.metadata
writer.add_metadata(metadata)

# Format the current date and time for the metadata
utc_time = '\05505\04700\047' # UTC time optional
time = datetime.now().strftime(f'D\072%Y%m%d%H%M%S{utc_time}')

# Add the new metadata
writer.add_metadata(
    {
        "/Author": "Martin",
        "/Producer": "Libre Writer",
        '/Title': 'IneffableTitle',
        '/Subject': "IneffableSubject",
        '/Keywords': 'IneffableKeywords',
        '/CreationDate': time,
        '/ModDate': time,
        '/Creator': "IneffableCreator",
        '/CustomField': 'IneffableCustomField',
    }
)

# Save the new PDF to a file
with open("meta-pdf.pdf", "wb") as f:
    writer.write(f)
```
