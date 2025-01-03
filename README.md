# qubecrawl

qubecrawl is essentially a lightweight wrapper around html2text, designed to enhance its functionality for LLM-friendly workflows. It builds on the core capabilities of html2text by adding features like user defined patterns for cleaning unwanted elements, flexible parsing by tags, classes, or IDs, and asynchronous metadata fetching. This makes it a focused solution for converting HTML into clean Markdown, tailored for seamless integration with modern applications like web scraping and data preparation for Large Language Models. 


<div style="text-align: center;">
  ![](https://github.com/Adhishtanaka/qubecrawl/blob/main/logo.png)
</div>


## Features  

- **HTML to Markdown Conversion**: Converts HTML content to clean Markdown with options to ignore links or images.   
- **Flexible Parsing Options**:  
  - Extract content by `class` or `id`.  
  - Parse main content elements like `<main>` or `<article>`.  
- **Customizable Cleaning Rules**: Add, remove, or clear cleaning patterns to suit your specific needs.  
- **Image URL Resolution**: Automatically resolves relative image URLs to absolute paths.  
- **Webpage Metadata and Headers Fetching**: Retrieve head data such as `<title>`, `<meta>`, and linked assets asynchronously.  

## qubecrawl in Action

qubecrawl makes website code easily readable in Markdown format, unlike plain HTML, by removing unwanted elements like navigation bars, footers, ads, and modals using predefined patterns.

![qubecrawl in action](./webscrap.gif)

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