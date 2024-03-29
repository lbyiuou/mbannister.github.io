---
layout: default
title: "CS 181M: Computational photography"
term: "Fall"
year: 2015
syllabus: true
---

# CS 181M: Computational photography

## Pomona College, Fall 2015
---

## Instructor, lectures and office hours
Instructor: Michael J. Bannister  
Office: Edmund's Hall 230  
Email: michael.bannister@pomona.edu  
Office hours: T W 4pm--6pm, Th 10am--11:45am  
Lectures: T Th 2:45pm--4:00pm in Edmund's Hall 101   
[Piazza discussion board](//piazza.com/pomona/fall2015/cs181m/home)

## Catalog description
Introduction to the mathematical and algorithmic techniques from image processing and computer vision via applications to computational photography. Computational photography is an exciting new field at the intersection of computer vision, graphics and machine learning. Its goal is to overcome the limitations of the traditional camera by using computational techniques to create, enhance, modify, and interpret digital images.

Topics may include: noise and blur reduction, warping and morphing, hole-filling, panoramic photo stitching, matting and blending, high dynamic range imaging and texture synthesis.

Prerequisites: CSCI055 PO (Discrete Math), CSCI062 PO (Data Structures), and MATH060 PO (Linear Algebra).

## Textbooks and other resources

_Computer Vision: Algorithms and Applications_
by [Richard Szeliski](//research.microsoft.com/en-us/um/people/szeliski/)  
Springer, ISBN 978-1-84882-935-0. [PDF @ Springer Link](//doi.org/10.1007/978-1-84882-935-0)

_Multiple View Geometry in Computer Vision_
by Richard Hartley and Andrew Zisserman  
Cambridge, ISBN 978-0-521-54051-3. [PDF @ Worldcat](//ccl.on.worldcat.org/oclc/171123855?databaseList=1708,239,245,251,638)

[MATLAB Documentation](//www.mathworks.com/help/matlab/)

### Software
For the assignments in this course you will be using [MATLAB](//www.mathworks.com/products/matlab/) or [GNU OCTAVE](//www.gnu.org/software/octave/). MATLAB is a commercial software package used for scientific computing, and GNU OCTAVE is a free alternative. The college has a license which allows students in the course to install MATLAB on their home computers, and it is installed on all lab computers. In addition, the college has access to [lynda.com](//www.lynda.com) video tutorials for MATLAB. _Students may, with instructor permission, choose to do their assignments in another language, but this is not recommended._ Please place a comment at the top of every assignment, specifying which language you are using and the specifications (OS, CPU and RAM) of the testing computer.

Some tasks (e.g. importing, cropping and resizing) are more easily done in photo editing software. We have installed [Adobe Photoshop](//www.adobe.com/products/photoshop.html) on the lab computers, and you may wish to install [GIMP](//www.gimp.org) (a free alternative to Photoshop) on your personal computer.

__Update(9/8):__ If you are working with images from your own camera, you may desire low level access to the RAW data your camera captures. To get this data you need to set it to save RAW image files---I recommend you also have it save a jpg file. This is not possible on all camera, and if you are unsure of how to set this option come by office hours. To work with these file with full control you can use a program called [dcraw](https://www.cybercom.net/~dcoffin/dcraw/).

## Grading

Your grade in the course is a weighted average of your grades on the assigned experiments and projects, as follows:

- Experiments: 15% (~1% each)
- Projects 1--4: 60% (15% each)
- Project 5: 25%

The conversion to letter grades will be determined at the end of the course.

## Experiments
There will be approximately fifteen short programming experiments, each of which should take no more than an hour to complete. The purpose of these experiments is to gain intuition for the material covered in class and to learn to use MATLAB. You may work together when working on the experiments, but it is expected that any code or text you turn in was typed by you and not "copy and pasted" from another student or other source.

- [Experiment 1: Color to black and white](experiment01.html) ([Solution](experiment01_sol.m))
- [Experiment 2: Demosaicing with bilinear interpolation](experiment02.html)
- [Experiment 3: Noisy Gnomes](experiment03.html)

<!-- -->

## Projects
There will be five projects, each of which will require a substantial time investment. __Start the projects early!__ The purpose of the projects is to gain a deep understanding for the challenges of implementing some of the methods presented in class. For the final project (Project 5) you will be free to choose the topic. In addition, you will be giving an in class presentation on Project 5. Projects 1 to 4 will be pair programming projects, and project 5 will be done in groups of two or three students.

- [Project 1: Images of the Russian empire](project01.html)
- [Project 2: Fun with frequencies](project02.html)
- [Project 3: Photo mosaics (panoramas)](project03.html)
- [Project 4: 3D Reconstruction](project04.html)
- [Project 5: Final project](project05.html)

## Examples
I will place code examples from class here.

- [Example 1: Fourier domain manipulation](example01.zip)
- [Example 2: Interpolation Demo](interp_demo.zip)

## Schedule

The following schedule is to be considered tentative, and will likely change during the semester. Please inform me of any inconsistencies that you notice. Links for sample code, and additional readings will be placed in the schedule. The lecture slides will be available on Piazza.

- Week 1
  - Tuesday (9/1): Introduction  
    Szeliski: 1.1, 1.2; Lynda.com URM (up and running with MATLAB): 0-2
  - Thursday (9/3): Digital photography  
    Szeliski: 2.1 (mostly 2.1.5), 2.2 (mostly 2.2.3); Lynda.com URM: 3-5
- Week 2
  - Tuesday (9/8): Sensors and color  
    Szeliski: 2.3
  - Thursday (9/10): Point operators and linear filtering  
    Szeliski: 3.1, 3.2
- Week 3
  - Tuesday (9/15): Image transformations and warping  
    Szeliski: 2.1, 3.6
  - Thursday (9/17): Morphing and Fourier transforms  
    Szeliski: 3.6, 3.4
- Week 4
  - Tuesday (9/22): Laplacian blending and compositing  
    Szeliski: 3.5
  - Thursday (9/24): __No class__  
    Go outside and take some picture!
  - Sunday (9/27): __Project 1 due!__
- Week 5
  - Tuesday (9/29): Details of Laplacian blending and overview of Poisson blending  
    Szeliski: 3.5, 9.3
  - Thursday (10/1): Homographies <!-- TODO: fit in Matting -->  
    Szeliski: 2.1, 9.1, 9.2
- Week 6
  - Tuesday (10/6): Automatic Correspondence for Mosaics  
    Szeliski: 6.1
  - Thursday (10/8): Singular Value Decomposition (theory and practice)
- Week 7:
  - Tuesday (10/13): Texture and histograms  
    Szeliski: 10.5
  - Thursday (10/15): Texture and stitching  
    Szeliski: 10.5
- Week 8: Texture synthesis
  - Tuesday (10/20): __No class__
  - Thursday (10/22): Stereo geometry  
    Szeliski: 11; HZ: 6, 9, 10
- Week 9:
  - Tuesday (10/27): More on stereo geometry  
    Szeliski: 11; HZ: 6, 9, 10
  - Thursday (10/29): Overview of high dynamic range photography and tone mapping
- Week 10:
  - Tuesday (11/3): Object Recognition
  - Thursday (11/5): Object recognition; Practical aspects of 3D reconstruction for Project 4  
    Szeliski: 11; HZ: 7, 11
- Week 11: Image segmentation
  - Tuesday (11/10):
  - Thursday (11/12):
- Week 12:
  - Tuesday (11/17): Single view 3D reconstruction.
  - Thursday (11/19): More single view 3D reconstruction and Project 5 ideas.
- Week 13:
  - Tuesday (11/24): Colorization
  - Thursday (11/26): __No class__
- Week 14
  - Tuesday (12/1): Coded aperture photography
  - Thursday (12/3): Something fun!
- Week 15
  - Tuesday (12/8): __Presentations__
  - Thursday (12/10): __No class__
- Finals Week
  - Thursday (12/17): __No exam__,

## External links
I will add relevant link to other pages here.

- [Light L16 Camera](https://light.co)
- [The Five Pillars of Exposure (video)](https://www.youtube.com/watch?v=c9ZwMuP1vQg)
- [The Truth About Lenses and Perspective (video)](https://www.youtube.com/watch?v=FP3kvSbN8q0)
- [Demystifying the Inverse Square Law (video)](https://www.youtube.com/watch?v=hjIKwOdfPMw)
- [The Late Show with Stephen Colbert Intro, using tilt-shift lens? (video)](https://www.youtube.com/watch?v=Wf4_bcrJ864)
- [An Intuitive Explanation of Fourier Theory](http://cns-alumni.bu.edu/~slehar/fourier/fourier.html)

## Collaboration and Academic Honesty Policy
As a student in this course, you are expected to understand and follow the academic honest policies of Pomona College (or your home campus) and the Department of Computer Science. Please take a few minutes to familiarize yourself with these policies:
[Department of Computer Science Academic Honesty Policy](//www.cs.pomona.edu/academichonesty); [Pomona College Academic Honesty Policy](http://catalog.pomona.edu/content.php?catoid=7&navoid=394).
Unless the instructions for an assignment explicitly allow a form of collaboration, assume that the standard academic honesty policies apply. If for any reason you do not understand how the academic policies apply to a particular course or assignment, discuss your concerns with the teaching staff for the course.

Submitted code may be analyzed by automated plagiarism detection software, which detects structural similarities in your code with other students submitted code (this quarter and in the past) and code available on Internet repositories.

All __exams__ will be closed-note, closed-book, closed-computer and individual effort.

If you do not abide by the academic honest policies, expect severe __penalties__. The first offense will result in failure in the course and will be reported to the Dean of Students Office. In the event of a second offense, the offense will be reported to the Board of Academic Discipline. For further explanation of the penalties see the academic honest policies linked above.

## Academic Accommodations
If you are seeking academic accommodations, you must contact your home college's disability coordinator to establish accommodations. You should plan to meet with your coordinator to discuss appropriate accommodations and may be asked to provide documentation necessary to verify disabilities. The disability coordinators for the Claremont Colleges are:
<a href='mailto:Jan.Collins-Eaglin@pomona.edu'>Jan Collins-Eaglin (Pomona)</a>,
<a href='mailto:julia.easley@claremontmckenna.edu'>Julia Easley (CMC)</a>,
<a href='mailto:Jill_Hawthorne@pitzer.edu'>Jill Hawthorne (Pitzer)</a>,
<a href='mailto:sdelator@scrippscollege.edu'>Sonia De la Torre Iniguez (Scripps)</a> and
<a href='mailto:hbird@hmc.edu'>Heidi Bird (HMC)</a>.

## Recording
Pomona College prohibits video or voice recording of any lecture or discussion, except in cases that the office of the Dean of Students has granted a student permission according to the College’s Disability Accommodations Policy, or when permission is granted by the instructor. I choose to give permission in this course to be recorded by students. These recordings are for any reasonable use that arises from participation in this course. __These recordings cannot be distributed, transmitted or published in any media or form, nor be used for any commercial purposes.__

## Acknowledgments
The design of this course is in large part based on similar courses offered by:
[Chuck Dyer @ UW](//pages.cs.wisc.edu/~dyer/cs534/index.html),
[Alexei Efros @ UCB](//inst.eecs.berkeley.edu/~cs194-26/fa14/),
[Charless Fowlkes @ UCI](//www.ics.uci.edu/~fowlkes/class/cs116/),
[James Hays @ Brown](//cs.brown.edu/courses/cs129/),
[Kris Kitani @ CMU](//graphics.cs.cmu.edu/courses/15-463/2014_fall/) and
[Svetlana Lazebnik @ UNC](//www.cs.unc.edu/~lazebnik/research/fall08/)
