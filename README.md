# AMPLab 2025: Collaborative Filtering with ListenBrainz Data

This project implements a collaborative filtering recommendation system using music listening data from ListenBrainz. The system processes a large-scale data of music listening records to build an artist recommendation model.

## Project Overview

The project consists of two main parts:
1. **Data Processing**: Processing and transforming raw ListenBrainz data into a format suitable for collaborative filtering
2. **Collaborative Filtering Model**: Building and using an implicit feedback recommendation system to suggest similar artists and make user recommendations

## Features

- Process large-scale compressed music listening data (12 months of ListenBrainz data)
- Map recording MSIDs to canonical MusicBrainz IDs for standardization
- Build user-artist interaction matrices from listening history
- Generate artist similarity recommendations
- Provide personalized artist recommendations for users
- batch recommendations for multiple users

## Project Structure

```
├── AMPLab_Colabfilter_Madhav.ipynb    # Main Jupyter notebook 
├── listenbrainz_model.py              # Core collaborative filtering functions

```

## Requirements

### Python Dependencies
```bash
pip install implicit numpy scipy h5py pandas pathlib tqdm zstandard
```

### System Requirements
- Python 3.7+
- At least 8GB RAM (16GB+ recommended for full dataset)
- 50GB+ free disk space for data processing
- `zstd` command-line tool for decompression

### Data Files Required
- `1.listens.zst` through `12.listens.zst` - Monthly listening data
- `listenbrainz_msid_mapping.csv-001.zst` - MSID to MBID mapping
- `canonical_recording_redirect.csv.zst` - Canonical recording redirects
- `canonical_musicbrainz_data.csv.zst` - Recording metadata
- `musicbrainz_artist.csv` - Artist information

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd assignment_02
```

2. Install dependencies:
```bash
pip install implicit numpy scipy h5py pandas pathlib tqdm zstandard
```

3. Set up data directories in the notebook:
   - Update `data_root` to point to your ListenBrainz data location
   - Ensure `working_root` and `scratch_root` directories exist

## Usage

**Note on Reproducibility**:
- This project may not be fully reproducible because the dataset used is not publicly available and cannot be uploaded or shared due to or size constraints.
Please refer to the code and methodology for implementation details. It can be reproduced If you have access to a similar dataset from ListenBrainz or anywhere else.

## Data Processing Pipeline

1. **Extract User-Recording Pairs**: Parse compressed JSON listening data
2. **MSID to MBID Mapping**: Convert recording MSIDs to canonical MusicBrainz IDs
3. **Canonical Redirects**: Apply canonical recording redirects
4. **Artist Mapping**: Map recordings to primary artists
5. **Play Count Aggregation**: Count plays per user-artist pair
6. **Matrix Creation**: Build sparse interaction matrix for collaborative filtering

## Model Details

- **Algorithm**: Alternating Least Squares (ALS) with implicit feedback
- **Matrix Weighting**: BM25 weighting to handle popularity bias
- **Factors**: 64 latent factors
- **Regularization**: 0.05
- **Alpha**: 2.0 (confidence scaling)

## Performance Considerations

- **Memory Management**: Large datasets are processed in chunks to avoid memory issues
- **Disk Space**: Temporary files are cleaned up during processing
- **Processing Time**: Full pipeline takes several hours depending on hardware

## Example Results

The system can identify similar artists and make personalized recommendations:
- Similar artists to Pink Floyd: Progressive rock and classic rock artists
- User recommendations: Based on listening history and collaborative patterns

## Troubleshooting

- **Memory Issues**: Reduce batch sizes or process data in smaller chunks
- **Missing Dependencies**: Ensure all Python packages are installed
- **Data Path Issues**: Verify data directory paths are correct
- **Decompression Issues**: Ensure `zstd` is installed and accessible

## License

This project is part of the AMPLab 2025 coursework on processing large datasets and collaborative filtering part of the Master's in Sound and Music Computing at UPF Barcelona. 
