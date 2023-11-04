# Lab 3 - Bugs and Commands
**Daniel Andrews**  

**Part 1 - Bugs**  
Example of failure-inducing input for the buggy program:  
```
@Test 
public void testReverseInPlaceFail() {
    int[] input1 = { 3 , 2, 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1 , 2 , 3 }, input1);
}
```
Example of non failure-inducing input for the buggy program:  
```
@Test
public void testReverseInPlacePass() {
    int[] input1 = { 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1 }, input1);
}
```
The result of running the tests showing what symptoms we can see:  
![image1](https://thedonutdan.github.io/cse15l-lab-reports/testresultslab3.png)  
Identifying the bug:  
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
        arr[i] = arr[arr.length - i - 1];
    }
}
```
In it's current iteration this method will replace each element with the element that is equidistant and opposite from the middle index of the array, however it takes no care to preserve the original elements of the array before it overwrites them. This causes the array to be returned with only the elements of the first half mirrored on either side of the middle element.  
Fixing the bug:  
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
        int temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i -1] = temp;
    }
}
```
Here we have added two lines to the method. The first line creates a temporary variable in which we can store the ith value in the array. Then we can replace the ith element with the element opposite and equidistant from the middle index of the array. Because we have preserved the ith value in the temp variable we can then overwrite the higher indexed value properly. We also have changed the loop to iterate only over the first half of the array as we will swap each element in the first and second half of the array. Note that iterating over the full array would result in the array being reversed twice, returning the original array and causing another bug.  

**Part 2 - Researching Commands**  
For this section of the lab I will be researching the `grep` command using `man grep` and I will show four options that can be used with `grep`. The working directory we will be using is the `/technical` directory from lab 2. Each example was researched using the command `man grep` on Cygwin 64 for Windows.

First option: `-i`  
The `-i` option for the `grep` command tells `grep` to run a case-insensitive search using the provided pattern.  

`-i` Example one:  
```
andre@Daniel MINGW64 ~/OneDrive/Documents/GitHub/docsearch/technical/911report (main)
$ grep -i shot *.txt
chapter-1.txt:    Minutes went by and word arrived of an aircraft down in Pennsylvania. 
Those in the shelter wondered if the aircraft had been shot down pursuant to this authorization.
chapter-1.txt:    NORAD officials have maintained that they would have intercepted and shot down United 93. We are not so sure. We are sure that the nation owes a debt to the passengers of United 93. Their actions saved the lives of countless others, and may have 
saved either the Capitol or the White House from destruction.
chapter-13.2.txt:            59. See FAA report, "Report of Aircraft Accident," Nov. 13, 2001; John Hendershot
chapter-13.2.txt:                2004). Experts told us that a gunshot would definitely 
be audible on the CVR. The
chapter-13.2.txt:            146. John Hendershot interview (Dec. 22, 2003).
chapter-13.2.txt:                aircraft could be shot down. See, e.g., DOD notes, Stephen Cambone notes, Sept. 11,
chapter-13.3.txt:                report, "ATF Snapshot," Jan. 30, 1998 (online at www.atf.gov/about/snap1998.htm).
chapter-13.4.txt:                24, 2004). Of the two operatives, only Mihdhar appears 
briefly on the video shot by
chapter-13.5.txt:                White House to kill the president. The man was shot by 
police and then killed
chapter-3.txt:                course of a long night, two Black Hawk helicopters were shot down, 73 Americans were
chapter-3.txt:                Kansi, an Islamic extremist from Pakistan, shot and killed two CIA employees at the
chapter-3.txt:                Bin Ladin, he said, "would have caused us a hell of a problem, but it was a shot we
chapter-3.txt:                Zinni said, "It was easy to take the shot from Washington 
and walk away from it. We
chapter-3.txt:            The idea, however, was a long shot. Bin Ladin's usual base of 
activity was near
chapter-6.txt:                might be shot down, and warned Clarke that a shootdown would be a "bonanza" for Bin
chapter-6.txt:                letting Americans openly carry long guns (rifles, shotguns, automatic weapons).
chapter-6.txt:                Tenet ticked off key questions: What is the chain of command? Who takes the shot?
chapter-7.txt:                impossible and increasing the likelihood that any plane would be shot down before
chapter-9.txt:            A jet fuel fireball erupted upon impact and shot down at least one bank of elevators.
```
Here we can see the use of the `-i` option for `grep` which will return all case non-sensitive occurences of the pattern provided. This can be useful when capitalization is unimportant to what information we are looking to find. In this case, we are searching the `/911reports` subdirectory for any instance of "shot" which will give us information on reports that may have involved a firearm.  
`-i` Example two:  
```
$ grep -i budget government/env_prot_agen/*.txt
government/env_prot_agen/bill.txt:''Subpart 3-Ozone Season NOx Budget Program
government/env_prot_agen/bill.txt:SUBPART 3. OZONE SEASON NOx BUDGET PROGRAM.
government/env_prot_agen/bill.txt:requirements, including the State's nitrogen oxides budget and
government/env_prot_agen/final.txt:NOx Budget Trading Program beginning May 1, 2003.    
government/env_prot_agen/final.txt:Budget Program). The revised ozone NAAQS and new PM2.5 NAAQS could
government/env_prot_agen/section-by-section_summary.txt:allowances covering emissions. Subpart 3 codifies the budgets and
government/env_prot_agen/section-by-section_summary.txt:Subpart 3. Ozone Season NOx Budget Program
government/env_prot_agen/section-by-section_summary.txt:trading budgets; the criteria for classifying cogeneration units as
government/env_prot_agen/section-by-section_summary.txt:administer the ozone season NOx 
budget trading program under the
government/env_prot_agen/section-by-section_summary.txt:allowances under the NOx budget 
trading program administered by the
```
Here we are searching the `governemnt/env_prot_agen/` subdirectories for any text files with information about budget. Again, in this case, it is not important to match capitalization as we don't care about the difference between the words "Budget" and "budget," we are simply looking for any mention of the word that may give us insight into the EPA's budget.  

Second option: `-c`  
The `-c` option for `grep` will suppress the usual output of the command and instead print out a count of occurrences of the pattern in each file. If we just wanted to see which files mention a certain phrase this can be useful.  
`-c` Example one:  
```
$ grep -c budget government/env_prot_agen/*.txt
government/env_prot_agen/1-3_meth_901.txt:0
government/env_prot_agen/atx1-6.txt:0      
government/env_prot_agen/bill.txt:1  
government/env_prot_agen/ctf1-6.txt:0
government/env_prot_agen/ctf7-10.txt:0
government/env_prot_agen/ctm4-10.txt:0
government/env_prot_agen/final.txt:0
government/env_prot_agen/jeffordslieberm.txt:0
government/env_prot_agen/multi102902.txt:0
government/env_prot_agen/nov1.txt:0
government/env_prot_agen/ro_clear_skies_book.txt:0
government/env_prot_agen/section-by-section_summary.txt:4
government/env_prot_agen/tech_adden.txt:0
government/env_prot_agen/tech_sectiong.txt:0
```
Here we can see that we won't be told what the line says that we have matched patterns on, but it can be useful to instead just be told which files had matching lines. Then we can find that file and examine it more closely for the information we need. In this case, maybe we just want to figure out which of the EPA related files mentions budget.  
`-c` Example two:  
```
$ grep -c shot 911report/*.txt
911report/chapter-1.txt:2
911report/chapter-10.txt:0
911report/chapter-11.txt:0
911report/chapter-12.txt:0
911report/chapter-13.1.txt:0
911report/chapter-13.2.txt:4
911report/chapter-13.3.txt:1
911report/chapter-13.4.txt:1
911report/chapter-13.5.txt:1
911report/chapter-2.txt:0
911report/chapter-3.txt:5
911report/chapter-5.txt:0
911report/chapter-6.txt:3
911report/chapter-7.txt:1
911report/chapter-8.txt:0
911report/chapter-9.txt:1
911report/preface.txt:0
```
Here is another example using the `-c` option. In this case maybe we just want to see which reports contain the given pattern rather than seeing the full printout of the line that matches. This can be useful as it is a more concise summary of what files match the pattern without loading our screen up with too much unnecessary information.  

Third option: `-m <num>`  
The `-m` option will stop scanning a file after reaching `num` amount of lines.  

`-m` Example one:  
```
$ grep -m 3 fruitflies biomed/*.txt
biomed/1471-2148-3-3.txt:        on fruitflies [ 30 61 ] and a unicellular alga [ 20 ] (but
```
In this case we are specifying that `grep` only scan the first 3 lines of each file. This can be useful if we, for example, want to find reports that specifically mention fruitflies in the title. Then we may only scan the first few lines to see if we can find files that contain a matching pattern.  

`-m` Example two:  
```
andre@Daniel MINGW64 ~/OneDrive/Documents/GitHub/docsearch/technical (main)
$ grep -m 10 speed 911report/*.txt
911report/chapter-1.txt:    At 9:32, controllers at the Dulles Terminal Radar Approach Control "observed a primary radar target tracking eastbound at a high rate of speed." This was later determined to have been Flight 77.
911report/chapter-1.txt:    By all accounts, the first 46 minutes of Flight 93's cross-country trip proceeded routinely. Radio communications from the plane were normal. Heading, speed, and altitude ran according to plan. At 9:24, Ballinger's warning to United 93 
was received in the cockpit. Within two minutes, at 9:26, the pilot, Jason Dahl, responded with a note of puzzlement: "Ed, confirm latest mssg plz-Jason."
911report/chapter-1.txt:    The Command Center kept looking for American 77. At 9:21, it advised the Dulles terminal control facility, and Dulles urged its controllers to look 
for primary targets. At 9:32, they found one. Several of the Dulles controllers "observed a primary radar target tracking eastbound at a high rate of speed" and notified Reagan National Airport. FAA personnel at both Reagan National and Dulles airports notified the Secret Service. The aircraft's identity or type was unknown.
911report/chapter-10.txt:                Hanjour's high-speed dive into the Pentagon. He told us he recalled Iraqi support
911report/chapter-12.txt:                To balance this measure, programs to speed known travelers should be a higher
911report/chapter-12.txt:                    entry-exit screening system, including a single system for speeding qualified
911report/chapter-13.2.txt:            238. These estimates are based on analysis of Boeing 757 maximum operating speed
911report/chapter-13.2.txt:                maximum speed without regard to overspeed warnings, a straight-line path, and no
911report/chapter-13.2.txt:                target. The probable time frame allows for speeds consistent with the observed
911report/chapter-13.4.txt:                Hazmi received a speeding ticket in Oklahoma 
on April 1, 2001. Ibid. (citing
911report/chapter-5.txt:            In retrospect, the speed with which Atta, Shehhi, Jarrah, and Binalshibh became core
911report/chapter-7.txt:                midnight on September 8-9, Jarrah received a speeding ticket in Maryland as he
```
Here is another example. In this case we are scanning the first ten lines of each text file in `911reports/` to see if there is a mention of speed. This can be especially useful if we are scanning files with very high line counts and need to limit `grep` so it doesn't take forever searching through the files.  

Fourth option: `-q`  
This option will run `grep` quietly with no output to the standard output, exiting with code `0` if a match is found.  

`-q` Example one:  
```
$ grep -q -i gene biomed/*.txt

andre@Daniel MINGW64 ~/OneDrive/Documents/GitHub/docsearch/technical (main)
$ echo $?
0
```
Here we can see that running `grep` wrote nothing to the standard output. This seems like it would not give us much information, but by using the command `echo $?` we can print the exit code for the last program run, `grep` in this case, and see that it returned `0` meaning it found a match. Running this in verbose mode floods the screen with search results that could be too much to effectively process, sometimes we just want to know if the pattern matches without seeing the specific lines or even counts like with `-c`.  

`-q` Example two:  
```
$ grep -q  herpaderpa  biomed/*.txt

andre@Daniel MINGW64 ~/OneDrive/Documents/GitHub/docsearch/technical (main)
$ echo $?
1
```
In this case we gave a fairly non-sense pattern for `grep` to scan for so it would not find any matches. We can see that calling the command `echo $?` to retrieve the exit code tells us `grep` exited with a return code of `1` meaning it could not find any matches. This is very useful as sometimes we just want to check for the existence of a pattern without being overloaded with output.
