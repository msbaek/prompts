---
description: Convert files to Markdown using Microsoft MarkItDown
argument-hint: <file_path>
---

# MarkItDown File Converter

Convert various file formats to Markdown using Microsoft's MarkItDown library and save to ~/Downloads/mark-it-down directory.

## Supported File Formats

Microsoft MarkItDown supports:
- **Office Documents**: .docx, .pptx, .xlsx
- **PDF Files**: .pdf
- **Images**: Various formats (with OCR and EXIF metadata)
- **Audio Files**: Various formats (with speech transcription)
- **Web Files**: .html
- **Data Files**: .csv, .json, .xml

## Task

Convert the specified file ($ARGUMENTS) to Markdown format using the following Python script:

```python
#!/usr/bin/env python3
import os
import sys
import subprocess
from pathlib import Path
from datetime import datetime

def ensure_markitdown_installed():
    """Ensure markitdown is installed, install if not"""
    try:
        import markitdown
        print("✅ MarkItDown library is already installed")
        return True
    except ImportError:
        print("📦 Installing MarkItDown library...")
        try:
            subprocess.check_call([sys.executable, "-m", "pip", "install", "markitdown[all]"])
            print("✅ MarkItDown library installed successfully")
            return True
        except subprocess.CalledProcessError as e:
            print(f"❌ Failed to install MarkItDown: {e}")
            return False

def convert_file_to_markdown(file_path):
    """Convert file to markdown using MarkItDown"""
    from markitdown import MarkItDown
    
    # Validate input file
    input_file = Path(file_path).expanduser().resolve()
    if not input_file.exists():
        print(f"❌ File does not exist: {input_file}")
        return None
    
    if not input_file.is_file():
        print(f"❌ Path is not a file: {input_file}")
        return None
    
    print(f"🔄 Converting file: {input_file.name}")
    
    try:
        # Initialize MarkItDown
        md = MarkItDown()
        
        # Convert file
        result = md.convert(str(input_file))
        
        if not result or not result.text_content:
            print("❌ Conversion failed: No content generated")
            return None
            
        return result.text_content, input_file.stem
        
    except Exception as e:
        print(f"❌ Conversion error: {e}")
        return None

def save_markdown(content, original_filename):
    """Save markdown content to ~/Downloads/mark-it-down directory"""
    # Create output directory
    output_dir = Path.home() / "Downloads" / "mark-it-down"
    output_dir.mkdir(parents=True, exist_ok=True)
    
    # Generate output filename
    output_file = output_dir / f"{original_filename}.md"
    
    # Handle duplicate files
    if output_file.exists():
        timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
        output_file = output_dir / f"{original_filename}_{timestamp}.md"
    
    try:
        # Save content
        with open(output_file, 'w', encoding='utf-8') as f:
            f.write(content)
        
        print(f"✅ Markdown saved to: {output_file}")
        print(f"📄 File size: {len(content):,} characters")
        
        # Show file info
        file_stats = output_file.stat()
        print(f"💾 File size on disk: {file_stats.st_size:,} bytes")
        
        return str(output_file)
        
    except Exception as e:
        print(f"❌ Failed to save file: {e}")
        return None

def main():
    # Check if file path is provided
    if len(sys.argv) != 2:
        print("❌ Usage: python script.py <file_path>")
        sys.exit(1)
    
    file_path = sys.argv[1]
    
    print("🚀 Microsoft MarkItDown File Converter")
    print("=" * 50)
    
    # Step 1: Ensure MarkItDown is installed
    if not ensure_markitdown_installed():
        sys.exit(1)
    
    # Step 2: Convert file
    result = convert_file_to_markdown(file_path)
    if not result:
        sys.exit(1)
    
    content, filename = result
    
    # Step 3: Save markdown
    output_path = save_markdown(content, filename)
    if not output_path:
        sys.exit(1)
    
    print("=" * 50)
    print("🎉 Conversion completed successfully!")
    print(f"📁 Output location: {output_path}")

if __name__ == "__main__":
    main()
```

## Execution

Run the Python script with the provided file path:

```bash
python3 -c "
import os
import sys
import subprocess
from pathlib import Path
from datetime import datetime

def ensure_markitdown_installed():
    try:
        import markitdown
        print('✅ MarkItDown library is already installed')
        return True
    except ImportError:
        print('📦 Installing MarkItDown library...')
        try:
            subprocess.check_call([sys.executable, '-m', 'pip', 'install', 'markitdown[all]'])
            print('✅ MarkItDown library installed successfully')
            return True
        except subprocess.CalledProcessError as e:
            print(f'❌ Failed to install MarkItDown: {e}')
            return False

def convert_file_to_markdown(file_path):
    from markitdown import MarkItDown
    
    input_file = Path(file_path).expanduser().resolve()
    if not input_file.exists():
        print(f'❌ File does not exist: {input_file}')
        return None
    
    if not input_file.is_file():
        print(f'❌ Path is not a file: {input_file}')
        return None
    
    print(f'🔄 Converting file: {input_file.name}')
    
    try:
        md = MarkItDown()
        result = md.convert(str(input_file))
        
        if not result or not result.text_content:
            print('❌ Conversion failed: No content generated')
            return None
            
        return result.text_content, input_file.stem
        
    except Exception as e:
        print(f'❌ Conversion error: {e}')
        return None

def save_markdown(content, original_filename):
    output_dir = Path.home() / 'Downloads' / 'mark-it-down'
    output_dir.mkdir(parents=True, exist_ok=True)
    
    output_file = output_dir / f'{original_filename}.md'
    
    if output_file.exists():
        timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
        output_file = output_dir / f'{original_filename}_{timestamp}.md'
    
    try:
        with open(output_file, 'w', encoding='utf-8') as f:
            f.write(content)
        
        print(f'✅ Markdown saved to: {output_file}')
        print(f'📄 File size: {len(content):,} characters')
        
        file_stats = output_file.stat()
        print(f'💾 File size on disk: {file_stats.st_size:,} bytes')
        
        return str(output_file)
        
    except Exception as e:
        print(f'❌ Failed to save file: {e}')
        return None

def main():
    file_path = '$ARGUMENTS'
    
    print('🚀 Microsoft MarkItDown File Converter')
    print('=' * 50)
    
    if not ensure_markitdown_installed():
        sys.exit(1)
    
    result = convert_file_to_markdown(file_path)
    if not result:
        sys.exit(1)
    
    content, filename = result
    
    output_path = save_markdown(content, filename)
    if not output_path:
        sys.exit(1)
    
    print('=' * 50)
    print('🎉 Conversion completed successfully!')
    print(f'📁 Output location: {output_path}')

main()
"