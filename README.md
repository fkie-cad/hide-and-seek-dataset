# Hide and Seek Dataset

This repository contains a structured dataset of **data hiding techniques in file systems**.
Each technique is organized in its own directory containing the **file system image** and corresponding **JSON metadata** describing how and where the data was embedded.

The dataset is designed for forensic analysis, detection research, and the evaluation of hidden data recovery techniques.

## Dataset Structure

The dataset is organized into the following data hiding scenarios:

| Scenario | Directory | Description |
|----------|-----------|-------------|
| Scenario 1 | `scenario_1_file_slack` | Data hidden in general file slack space. |
| Scenario 2 | `scenario_2_timestamps` | Data hidden in file timestamps. |
| Scenario 3 | `scenario_3_bad_units` | Data hidden in bad units. |
| Scenario 4 | `scenario_4_additional_data_units` | Data hidden in additional data units. |
| Scenario 5 | `scenario_5_slack_space` | Data hidden in slack space structures. |
| Scenario 6 | `scenario_6_reserved_space` | Data hidden in reserved areas of structures. |
| Scenario 7 | `scenario_7_snapshots` | Data hidden in hidden snapshots. |
| Scenario 8 | `scenario_8_lower_file_slack` | Data hidden in lower file slack. |
| Scenario 9 | `scenario_9_pooled_storage_slack` | Data hidden in the slack space of physical members in pooled file systems. |

Each scenario directory contains forensic images and documentation for multiple file systems including:
**APFS**, **btrfs**, **exFAT**, **ext2**, **ext4**, **FAT**, **NTFS**, **MooseFS**, and **ZFS**.

### Directory Organization

Each hiding technique is organized in its own subdirectory with standardized file names:

```
scenario_X_<name>/
├── <technique_1>/
│   ├── metadata.json      # Ground truth documentation
│   └── image.img.gz       # Compressed forensic image file
├── <technique_2>/
│   ├── metadata.json
│   └── image.img.gz
└── ...
```

For techniques involving multiple devices (e.g., RAID configurations), images are named `dev1.img.gz`, `dev2.img.gz`, etc.:

```
scenario_9_pooled_storage_slack/
└── btrfs_raid1_slack/
    ├── metadata.json
    ├── dev1.img.gz
    └── dev2.img.gz
```

**Note:** All forensic images are compressed with gzip to save space. Decompress before use:
```bash
gunzip image.img.gz    # Decompresses to image.img
```

**Example directory names** follow the pattern `<filesystem>_<technique>` in lowercase with underscores:
- `apfs_file_slack`
- `ext4_timestamp`
- `fat_fsinfo_reserved`
- `ntfs_mft_slack`

## JSON Documentation Format

Each technique directory contains a `metadata.json` file that follows a structured format, including:
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
```

## Citation

This dataset accompanies the research paper:

> Schwietert, A., & Hilgert, J.-N. (2025). Data hiding in file systems: Current state, novel methods, and a standardized corpus. *Forensic Science International: Digital Investigation*, 54, 301984. Elsevier.

**Paper:** [https://www.sciencedirect.com/science/article/pii/S2666281725001246](https://www.sciencedirect.com/science/article/pii/S2666281725001246)

**BibTeX:**
```bibtex
@article{schwietert2025data,
  title={Data hiding in file systems: Current state, novel methods, and a standardized corpus},
  author={Schwietert, Anton and Hilgert, Jan-Niclas},
  journal={Forensic Science International: Digital Investigation},
  volume={54},
  pages={301984},
  year={2025},
  publisher={Elsevier}
}
```
