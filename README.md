# qubecrawl

qubecrawl is a lightweight Python library designed to make data conversion LLM-friendly, allowing for seamless web scraping and HTML-to-Markdown transformation. With qubecrawl, you can effortlessly extract, clean, and transform web content into Markdown format for easy integration into your workflows.  


<div style="text-align: center;">
  <img src="logo.png" alt="qubecrawl logo" />
</div>


## Features  

- **HTML to Markdown Conversion**: Converts HTML content to clean Markdown with options to ignore links or images.  
- **Content Cleaning**: Automatically removes unwanted elements like navigation bars, footers, ads, and modals using predefined patterns.  
- **Flexible Parsing Options**:  
  - Extract content by `class` or `id`.  
  - Parse main content elements like `<main>` or `<article>`.  
- **Customizable Cleaning Rules**: Add, remove, or clear cleaning patterns to suit your specific needs.  
- **Image URL Resolution**: Automatically resolves relative image URLs to absolute paths.  
- **Webpage Metadata and Headers Fetching**: Retrieve head data such as `<title>`, `<meta>`, and linked assets asynchronously.  

## Requirements  

- Python 3.8 or higher.  

## Installation  

```bash  
pip install qubecrawl 
```

## Usage

Here’s a quick example of how to use qubecrawl:

```python
import asyncio
import requests
from qubecrawl import qubecrawl 

# Initialize qubecrawlwith default settings  
crawler = qubecrawl()  

# Parse a webpage  
url = "https://example.com"  
response = requests.get(url)  
markdown = crawler.parse_(response.text, url)
print(markdown)  
  
# Parse content by class name  
class_name = "content-class"  
markdown_by_class = crawler.parse_class(response.text, class_name, url) 
print(markdown_by_class)

# Parse content by ID  
element_id = "unique-id"  
markdown_by_id = crawler.parse_id(response.text, element_id, url)  
print(markdown_by_id)  

# Fetch metadata & headers
json_file = asyncio.run(crawler.get_head(url))
print(json_file)

```

## Configuration

- **Custom Patterns**: You can add or remove patterns to fine-tune content cleaning.

  ```python
  #default patterns
   patterns = [
        "nav", "menu", "navbar", "sidebar", "drawer", "breadcrumb", "side-nav", "sidenav", "header", "footer", 
        "bottom-bar", "top-bar", "ad-", "ads-", "advertisement", "banner", "promo", "sponsored", "ads", "popup", 
        "modal", "overlay", "dialog", "toast", "alert", "notification", "tracking", "analytics", "pixel", "beacon", 
        "tag-manager", "disclaimer", "newsletter", "subscribe", "signup", "mailing-list", "search", "login", "register", 
        "sign-in", "cookie", "gdpr", "consent", "privacy", "terms", "copyright", "hidden", "display-none", "invisible", 
        "spacer", "gap", "background", "decoration", "ornament", "pattern", "gradient", "carousel", "slider", "lightbox", 
        "tooltip", "dropdown", "skeleton", "placeholder", "loading", "shimmer", "spinner"
    ]
    ```
  
  ```python
  crawler.add_pattern("custom-pattern") # Add custom pattern
  crawler.remove_pattern("nav") # Remove "nav" pattern
  crawler.get_patterns()   # Get all patterns
  crawler.clear_patterns() # Clear all patterns
  ```
- **Markdown Options**: Control the output by ignoring links, images, or unnessory elements using the qubecrawl constructor.
  
  ```python
  #default constuctor
  crawler = qubecrawl(ignore_links=True, ignore_img=False, clean=True)
  ```

## License

This extension is open source and available under the [MIT License](LICENSE).

## Contact

- **Author**: [Adhishtanaka](https://github.com/Adhishtanaka)
- **Email**: kulasoooriyaa@gmail.com

## Contributing

If you find any bugs or want to suggest improvements, feel free to open an issue or pull request on the [GitHub repository](https://github.com/Adhishtanaka/qubecrawl/pulls).