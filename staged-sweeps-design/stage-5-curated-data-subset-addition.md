# Stage 5 - data curation

This has two axis - first, I selected the highest quality low data to include in our training set. so i went to splits/training and pulled out all the low quality data. i ran this through stage4\_038 which was trained on  only high and medium quality data. then i took the top predictions for those files an pulled the files the top x% of filed in terms of RADR score to separate folders. this resulted i nthe 4 folders below:\
small: 51 (5%), medium: 154 (15%), large: 309 (30%), xl: 515 (50%)



Matched 1030 rows to files in D:\important\projects\Frog\scripts\BirdNET\_CustomClassifierSuite\scripts\input\
Selection sizes -> small: 51, medium: 154, large: 309, top50: 515\
Wrote 51 files to D:\important\projects\Frog\scripts\BirdNET\_CustomClassifierSuite\scripts\curated\small (0 linked/copied).\
Wrote 154 files to D:\important\projects\Frog\scripts\BirdNET\_CustomClassifierSuite\scripts\curated\medium (0 linked/copied).\
Wrote 309 files to D:\important\projects\Frog\scripts\BirdNET\_CustomClassifierSuite\scripts\curated\large (0 linked/copied).\
Wrote 515 files to D:\important\projects\Frog\scripts\BirdNET\_CustomClassifierSuite\scripts\curated\top50 (515 linked/copied).
