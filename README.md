Installation : Please read NGS-module readme file for installing miR-BAG on your local system. 


How to use miR-BAG GUI for sequence-scan module:
(a). File format
(b). Output destination
(c). Number of processors to be used
(d). Select Species model
(e). Filtering options
(f). Run miR-BAG  
(e). Run miR-BAG on command line.

(a). File format
User has to upload the input file which will be in fasta format  i.e. a single-line description (sequence ID), followed by the lines of sequence data. The sequence ID  always begins with the fasta header (>) and may not consist of any tabs. Sequence data must consist of a sequence of length  of 200bp at least. The sequence data can be in single line or in multiple lines. The following example shows the input file format for miR-BAG sequence scan module.
>ath-MIR156e 
GUCGAUAUCGGCUGUGGAGGACGACUAGCUACGGUUUCGAGCCUGGUCACAUGCGUAGAGUGUGAAAGGUAAUUAGGAGGUGACAGAAGAGAGUGAGCACACAUGGUGGUUUCUUGCAUGCUUUUUUGAUUAGGGUUUCAUGCUUGAAGCUAUGUGUGCUUACUCUCUCUCUGUCACCCCUUCUCUCUCUCUCUCUUUUC

Also  sequence data only consist of  A, T/U, G, C bases only. So please check all the sequences before uploading the seuence file.
The user can submit any number of sequences in the input file in the above mentioned format where each sequence is seperated by a new line. For e.g.

>ath-MIR156e 
GUCGAUAUCGGCUGUGGAGGACGACUAGCUACGGUUUCGAGCCUGGUCACAU
GCGUAGAGUGUGAAAGGUAAUUAGGAGGUGACAGAAGAGAGUGAGCACACA
UGGUGGUUUCUUGCAUGCUUUUUUGAUUAGGGUUUCAUGCUUGAAGCUAUG
UGUGCUUACUCUCUCUCUGUCACCCCUUCUCUCUCUCUCUCUUUUC
>ath-MIR156f 
GGCUAGGGUUUAUAGAUGUAUGUGAUAUUAAGAGAUAUGAAACAUAUUUGU
CGACGGUUUGAGUGGUGAGGAAUUGAUGGUGACAGAAGAGAGUGAGCACAC
AUGGUGGCUUUCUUGCAUAUUUGAAGGUUCCAUGCUUGAAGCUAUGUGUGCU
CACUCUCUAUCCGUCACCCCCUUCUCUCCCUCUCCCUCUCUCUCUC


(b).Output destination
User has to select an output destination directory. All the intermediate files and result files are created in this directory. Once miR-BAG is executed completely two result file with name            "miR-BAG_result_file" and "miR-BAG_result_file_complementary" are created in this directory.
The "miR-BAG_result_file" consist of sequence ID, start position of best precursor sequence found, end position of best precursor sequence found, best precursor sequence of length 200bp and classification score. Only those sequences are given in the miR-BAG_result_file which has classification score 0.333 and above.
In miR-BAG three classifiers named Support Vector Machine (SVM), Naive Bayes (NB) and Best First Decision Trees (BFTree) are used for classification. The score 0.333 indicates  that one classifier classifies the submitted sequence as positive candidate, score 0.666 indicates two classifiers classifies the submitted sequence as positive candidate and score 1.0 indicates all three classifiers classifies  the submitted sequence as positive candidate.
As miR-BAG also accept sequences with length above 200bp and work on sliding fragments of length 200bp. If sequence length is greater than 200bp then best precursor sequence of length 200bp with highest classification score 100bp upstream and 100bp downstream is given in the  miR-BAG_result_file. The                 "miR-BAG_result_file_complementary" has the result of corresponding reverse complementary sequences.

c). Number of processors to be used
miR-BAG is created as multithreaded concurrent application to reduce the computation time. Parallelism is implemented on various levels in miR-BAG. So miR-BAG can be run on multiple processors. For high throughput execution user can select maximum number of 	processsors which are supported by user's machine. Be careful while selecting number of processors as selecting large number of processors which are not supported by user's machine will hang user's machine.

(d). Select Species model
As 6 different species were used in the study of miR-BAG,forming 6 different types of species models. User can select any one species model from these models to identify correct pre-miRNA candidates. 

(e). Filtering options
It seems that while working with sequence length of exactly 200bp the output is given 	instantly by miR-BAG. But if user submits a sequence of length above 200bp then miR-BAG has to work on sliding fragments of 200bp. So if user has submitted a seuence of length 300bp then miR-BAG has to compute the data on 100 fragments repeatedly. So in that case one sequence of lenght 300bp is eqivalent to 100 sequences of length 200bp for miR-BAG. This creation of fragments and computation of various features on these fragments takes alot of time. User can reduce the number of fragments by selecting different filtering options.Six filtering options are given in the standalone version of miR-BAG. User can check the particular checkbox of desired filter, then user has to select minimum cut-off value which  user can select from the vertical sliders. The minimum cut-off value is displayed at the bottom of each slider.The range for each filter is the minimum cut-off value selected by the user to the highest value of that filter. Different tables of statistics for each filtering option are given in the Readme.doc file. 
Note that while using each filter user fastens the execution at the cost of some accuracy.

(f). Run miR-BAG 
To run miR-BAG user has to click run button. A progress bar immediately appears after
making a click on run button. If user want to end miR-BAG click cancel button.

(e). Run miR-BAG on command line
 To run miR-BAG on command line first switch to "sequence" directory using cd command on terminal then use one of following two commands.
 (i). To run miR-BAG without any filtering options on command line we can use following command:
          java -jar Mirbag.jar input_file_name output_destination_directory no_of_processors_to_be_used species_model
For e.g.  java -jar Mirbag.jar input_file /output_destination 4 human
Note: User can give the name of species_model as: human for Homo sapiens, celegans for Caenorhabditis elegans, drosophila for Drosophila melanogaster, mouse for Mus Musculus, dog for Canis familiaris and rat for Rattus norvegicus.
(ii). To run miR-BAG with some filtering options on command line we can use following command:
java -jar Mirbag-filter.jar input_file_name output_destination_directory no_of_processors_to_be_used species_model total_no_of_filters_used MFE_filter_value Loop_size_filter_value stem_length_filter_value Bulge_distance_filter_value Mismatch_filter_value Distance_and_loop_based_filter_value
For e.g.  java -jar Mirbag-filter.jar input_file /output_destination 5 celegans 6 -100 15 60 30 5 5
Note: User can use any number of filtering options by providing a value between 1 to 6 as 5th argument to above command. Also if user do not want to use any filtering option then he/she has to enter 0 value as command line argument. For e.g. if you do not want to use "stem length" and "Mismatch" filters then our command will be as: 
 java -jar Mirbag-filter.jar input_file /output_destination 5 celegans 4 -100 15 0 30 0 5             


The standalone version of miR-BAG is available at: https://scbb.ihbt.res.in/SCBB_dept/images/miR_BAG.zip
