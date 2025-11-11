# Hide and Seek Dataset

This repository contains a structured dataset of **data hiding techniques in file systems**.  
Each subfolder represents a specific hiding method and includes both the **file system images** in which data was hidden and the corresponding **JSON documentation** describing how and where the data was embedded.

The dataset is designed for forensic analysis, detection research, and the evaluation of hidden data recovery techniques.

Each **`.zip`** file contains one or more file system images (`.img`) that were used to demonstrate a particular data hiding method.  
Each corresponding **`.json`** file documents the reconstruction process, the offsets where data was hidden, and additional notes.

## 🧾 JSON Documentation Format

Each `.json` documentation file follows a structured format, including:
- **notes:** General observations and reconstruction hints.  
- **file_info:** Metadata of the affected files or inodes.  
- **hidden_data_offsets:** Byte offsets and lengths where hidden data was inserted.  
- **description:** Short explanation of the hiding method used.  

Example (simplified):

```json
{
  "description": "Hidden data stored in file slack area between logical file end and physical cluster end.",
  "notes": "All offsets calculated with sector size 512 bytes.",
  "file_info": [
    {
      "inode": 11398,
      "filename": "file_001.txt",
      "size_bytes": 2048
    }
  ],
  "hidden_data_offsets": [
    {
      "offset_bytes": 1052672,
      "length_bytes": 64
    }
  ],
  "reconstruction": "Recover hidden bytes from specified offset region using hex extraction."
}
