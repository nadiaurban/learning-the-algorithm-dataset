# Learning the Algorithm: YouTube Creator Discourse Dataset

[![License](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

## Overview

This dataset contains transcripts of 179 YouTube videos in which content creators discuss the YouTube algorithm, platform visibility, and optimization strategies. The corpus was collected and analyzed for the paper:

> **"Learning the Algorithm: Responsibilization and the Limits of Agency on YouTube"**  
> [Nadia Urban], [2026]  


The dataset supports research on algorithmic folk theories, platform governance, creator labor, and computational discourse analysis.

---

## Dataset Contents

### 1. `youtube_algorithm.csv`

Main dataset containing video metadata and transcripts.

| Column | Type | Description |
|--------|------|-------------|
| `video_id` | string | YouTube video identifier (11-character code) |
| `title` | string | Video title as it appears on YouTube |
| `published` | datetime | Publication date and time (UTC) |
| `matched_term` | string | Search query that retrieved this video |
| `channel_id` | string | YouTube channel identifier |
| `view_count` | integer | Number of views at time of collection |
| `like_count` | float | Number of likes (may be null if disabled) |
| `comment_count` | float | Number of comments |
| `duration` | string | Video duration in ISO 8601 format (e.g., PT15M33S) |
| `subscribers` | integer | Channel subscriber count at time of collection |
| `total_channel_views` | integer | Total views across all videos on the channel |
| `total_videos` | integer | Total number of videos published by the channel |
| `language` | string | Detected language of transcript (ISO 639-1 code) |
| `transcript` | string | Full video transcript (auto-generated or manual captions) |

**Total records:** 179 videos  
**Collection method:** YouTube Data API v3

---

### 2. `codebook.csv`

Thematic framework used for discourse analysis.

| Column | Description |
|--------|-------------|
| `Theme` | Name of the algorithmic folk theory theme |
| `Explanatory Notes` | Conceptual definition and analytical interpretation |
| `Seed Quotes` | Representative sentences used as semantic anchors for classification |

**Total themes:** 8

The codebook documents the interpretive framework developed through iterative qualitative analysis. Seed quotes were used in semantic similarity classification to systematically assign sentences across the corpus to thematic categories.

---

## Data Collection

### Search Queries

Videos were identified using targeted search terms related to algorithmic visibility:
- "YouTube algorithm"
- "how the YouTube algorithm works"
- "beat the YouTube algorithm"
- "YouTube algorithm update"
- "My channel is dead"
- "why my views dropped"
- "grow on YouTube"


### Inclusion Criteria

Videos were included if they:
- Explicitly addressed YouTube's algorithmic systems
- Discussed visibility, reach, or ranking dynamics
- Were substantively focused on algorithmic issues (not merely mentioning them)
- Were in English
- Had sufficient transcript length for analysis

### Exclusion Criteria

- Transcripts shorter than 40 words.
- Non-English videos
- Videos where transcripts were unavailable or corrupted
- Videos focused on non-algorithmic topics

---

## Ethical Considerations

### Public Data

All videos in this dataset were publicly posted by creators who made their content searchable and discoverable on YouTube. Following established practice in digital methods research (franzke et al., 2020; Zimmer & Proferes, 2014), we treat these videos as **public discourse** rather than private or sensitive data.

### Why Identifiers Are Included

Video IDs and channel IDs are included to enable:
- **Verification:** Other researchers can confirm data collection procedures
- **Replication:** Thematic coding and analysis can be independently validated
- **Extension:** The dataset can be used for new research questions
- **Context:** Researchers can access original videos to understand full context

While channel names are not included in the dataset, videos remain identifiable through their IDs and can be accessed via standard YouTube URLs (`https://youtube.com/watch?v=[video_id]`).

### Creator Rights

**If you are a creator whose video appears in this dataset and wish to have it removed:**
- Contact: [nadzieja.urban@gmail.com]
- We will honor all removal requests promptly
- Removed videos will be documented in a changelog

### Research Ethics References

- franzke, a. s., Bechmann, A., Zimmer, M., Ess, C., & the Association of Internet Researchers. (2020). *Internet Research: Ethical Guidelines 3.0.* https://aoir.org/reports/ethics3.pdf
- Zimmer, M., & Proferes, N. J. (2014). A topology of Twitter research: Disciplines, methods, and ethics. *Aslib Journal of Information Management*, 66(3), 250-261.

---

## Usage Guidelines

### Recommended Practices

Researchers using this dataset should:

1. **Cite the original paper** when using this data
2. **Follow ethical guidelines** for digital research (AoIR, institutional IRB)
3. **Contextualize quotes appropriately** — avoid misrepresenting creator intent
4. **Respect creators as public communicators** — not as anonymous research subjects
5. **Consider recontextualization risks** — academic framing may differ from creators' intentions

### Citation

If you use this dataset, please cite both the dataset and the original paper:

**Dataset citation:**
```
Urban, N. (2026). Learning the Algorithm: YouTube Creator Discourse Dataset. https://doi.org/10.5281/zenodo.20482140

```
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20482140.svg)](https://doi.org/10.5281/zenodo.20482140)



**Paper citation:**
```
Urban, N. (2026). Learning the Algorithm: Responsibilization and the Limits of Agency.

```

---

## Replication & Extension

### Reproducing the Analysis

To replicate the findings in the paper:

1. Load `youtube_algorithm.csv` for transcript data
2. Load `codebook.csv` for thematic framework
3. Apply semantic similarity classification using seed quotes as anchors
4. Embedding model used: `all-mpnet-base-v2` (Sentence Transformers)
5. Similarity threshold: [0.45]
6. Classification method: Cosine similarity between sentence embeddings

Full methodological details are provided in the paper's methods section.

### Extending the Dataset

Researchers may extend this work by:
- Collecting additional videos using similar search queries
- Comparing discourse across different time periods
- Analyzing different platforms (TikTok, Instagram, Twitch)
- Examining creator demographics or channel characteristics
- Studying temporal evolution of algorithmic folk theories

---

## Technical Notes

### Transcript Quality

- Transcripts are sourced from YouTube's automatic captions or creator-uploaded captions
- Automatic captions may contain transcription errors
- Punctuation and capitalization may be inconsistent
- Non-speech sounds (music, applause) are typically not transcribed

### Duration Format

Duration is stored in ISO 8601 format. Example conversions:
- `PT15M33S` = 15 minutes, 33 seconds
- `PT1H2M15S` = 1 hour, 2 minutes, 15 seconds
- `PT45S` = 45 seconds

To parse in Python:
```python
import isodate
duration_seconds = isodate.parse_duration(row['duration']).total_seconds()
```

### Missing Values

- `like_count` may be null (2 videos) if likes were disabled by the creator
- All other fields have complete data

---

## Changelog

**Version 1.0** (2026-02-22)
- Initial release
- 179 videos posted between between February 2017 and November 2025
- 8 thematic categories identified

[Future updates will be documented here]

---

## License

This dataset is released under **Creative Commons Attribution 4.0 International (CC BY 4.0)**.

You are free to:
- **Share** — copy and redistribute the material
- **Adapt** — remix, transform, and build upon the material

Under the following terms:
- **Attribution** — You must give appropriate credit and indicate if changes were made

Note: Individual videos remain copyrighted by their creators. This license applies to the compiled dataset and metadata, not to the underlying video content.

Full license text: https://creativecommons.org/licenses/by/4.0/

---

## Contact

**Researcher:** Nadia Urban 
**Institution:** East China Normal University
**ORCID:** 0009-0001-6282-5919

For questions about the dataset, paper, or methodological details, please contact the author directly.

---


