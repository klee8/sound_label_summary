[![DOI](https://zenodo.org/badge/75901343.svg)](https://zenodo.org/badge/latestdoi/75901343)

# sum_label.pl written by Kate Lee
## April 2016

MIT Licenced

The script takes in files generated in Octave which label sound files based on a model of a particular species call. In order to reduce false positives, some rules were made to compare the output of different species models. This script goes through all the files together. It looks at the labels in a number of files which were generated by running the same soundfile through a number of models. The script identifies whenever there is a change in one of the files and evaluates the time block until the next change. The summary of labels is calculated using the rules laid out below by [Ivan Braga Campos](https://unidirectory.auckland.ac.nz/people/profile/icam765). A summary file with these block and their start and end times are printed to output file.

The script takes in two files. An input file which contains a list of all the model files to sum, one on each line (default input file is sum_me.txt) and categories.txt which contains a list of all the categories, one on each line (i.e. the bird models and 'noise', 'background' and 'other_sb')


usage :
perl sum_label.pl

or

perl sum_label.pl \<inputfile\> \<outfile\>


The rules I have used doing this summary are:

 1. When the five labels are indicating the same category, use that category
       -(example1: five models indicating “background”)
       -(example2:  five models indicating “other_sb”)
 2. The  “background” label should be used every time it appears in at least one of the five models, with two exceptions:
       -Exception 1:  when “background” appears at the same time as “noise” – use “noise” in this case.
       -Exception 2:  when “background” appears at the same time as two different bird species – use “unidentified” in this case.
 3. The “noise” label should be used every time it appear in one of the five models.
 4. When there are 2 categories indicated among the five models and one of the categories is a bird species and the other is “other_sb”, 
    use the bird species label (ex: one model indicate GFP and all the others indicate “other_sb” = the GFP label should be used)
 5. When there are 3 categories indicated among the five models, use the category "unidentified”.(example: two of the categories are bird
    	 species and the other is “other_sb” or “background”).
     5A: Note that in this case the “unidentified” label should be used from the beginning of the bird species which started first and go 
     	 until the end of the second species.
 6. When there are 4 categories among the five models use “unidentified”.
 7. Replace "other_sb" label with "unidentified"


## running the example

enter the example folder and run sum_label.pl
<pre><code> cd example
    perl ../sum_label.pl
</code></pre>

### outfile (default: summary.labels.txt)
shows a list of each time block and the summarised label for that block

### label.log
Indicates the timeframe looked at and categories used.
Shows how the program is making decisions in each block (between underscored lines).
Each block shows the current timeslot and label for each of the files, what has been printed for the last block (in the starred line), and the decision for the current block.

