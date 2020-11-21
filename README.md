# CheXpert-review
Results of an amateur manual review of the CheXpert dataset

Overall: 688 (0.3%) images were excluded and 155 (0.07%) images were edited.

train-ayhyap.csv contains the 'Path' column from the original train.csv, and 3 columns extra columns: exclude, edited and note.

'exclude' (1 or blank) indicates whether the image should be excluded.
'edited' (1 or blank) indicates whether the image should be edited.
'note' (string) indicates the reason for exclusion, or the edit required.

Count Reason
354   incomplete
244   striped
25    corrupted
25    obstructed
23    poor
6     non-cxr
4     quantized
4     posture

[Comments on exclusion reasoning]
Incomplete: The image contains under 60%-70% of the chest area. As labels are generated on a study-level, it is possible for the label to refer to an area outside of the image.
Striped: The image contains a burst of rows has been shifted horizontally with wraparound. (there is actually more nuance to this, and fixing it is nontrivial)
Corrupted: The image appears corrupted in some way.
Obstructed: The image contains _abnormal_ obstructions.
Poor: The image quality is poor and diagnosis is impossible.
Non-CXR: The image is not a chest x-ray image at all. (mostly pelvic scans)
Quantized: The image's pixel values have been quantized, reducing effective bit-depth and making diagnosis impossible.
Posture: The patient's posture significantly complicates diagnosis. There were several patients with severe scoliosis (spine curved sideways) who could be excluded for this reason, but they have been left in.

The edits are all rotations to correct the orientation of the image.
They are of format: (angle) CW rotation
Rotations are in multiples of 90 degrees, and always clockwise.
Note that only Frontal images have this field labeled, Lateral images were skipped.
