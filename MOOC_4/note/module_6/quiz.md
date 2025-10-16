Non-Negative Matrix Factorization (NMF) & Dimensionality Reduction Recap

This section introduces Non-Negative Matrix Factorization (NMF) — a dimensionality reduction method that decomposes data into additive, interpretable components — and then summarizes how all dimensionality reduction techniques compare.
1. What is Non-Negative Matrix Factorization (NMF)?
<img width="1036" height="578" alt="image" src="https://github.com/user-attachments/assets/2c25d8d7-9027-43dd-8dda-c9c02d44ba66" />

NMF is a method for reducing dimensions only on non-negative data (no negative values).
Examples of suitable data:

Word counts (text data)

Pixel values (images)

Audio or video signal intensities

Mathematical Idea

Given a non-negative matrix 
𝐴
A,
we decompose it into two smaller non-negative matrices 
W and 𝐻
<img width="145" height="50" alt="image" src="https://github.com/user-attachments/assets/5390d1d6-576e-457f-b182-6c9dcf1efa32" />
Where:
W: represents latent features (e.g., topics, facial parts)
H: represents how those features combine to recreate the original data
Both 
W and H contain only positive values — meaning all components are additive, not subtractive.
<img width="1048" height="499" alt="image" src="https://github.com/user-attachments/assets/11a5a88a-6739-45dd-a834-dab15f78d8c0" />

