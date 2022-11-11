# The school choice project: summarization

### What has been done
- Created a GitHub repo to store the code and all findings of this project.
- Did Profiling on the code and detected the bottleneck.
- Changed the format of agent data files from Python pickle to GeoJSON to:
	- resolve dependency issue, and
	- make data human-readable.
- Cleaned up the code to make it more structured and easier to read.
- Modify/rewrite parts of the code to speed it up, see below:
	- Avoided recalculating the distance information when that is available by loading from files.
	- Moved storage of key agent metrices/properties from instances to shared memory of classes for speeding up memory allocation.
	- Vectorized some code that are considered as bottleneck using Numpy.
	- Improved speed of creating agents when loading the information from files.
- Investigated different Python compilers to see if they can help improving the runtime performance of the code 
	- Those compilers include PyPy, Numba, Cython, and MyPy.
	- Cython brings the biggest improvement. But by comparing the two cases (with/without Cython), it seems that the Cython gives even worse performance, see this [notebook](https://github.com/ODISSEI-School-Choice/school-choice/blob/gitlabmaster/cython_school_ranking/run.ipynb).
- Verified that the modified code works as expected.
	- The modified code passed all unit tests.
	- The modified code gave expected results on benchmark datasets.
- Adapted the code for enabling running multiple models at once with Dask.
- Documented our work.

### What has been achieved
- Benchmarking result:
	- We compared the performance of the old and new code on both the Amsterdam and Lattice cases.
	- Results show nearly 6 times faster running the Amsterdam case in a Windows Subsystem for Linux.
	- The same execution can be even faster in native linux (12 times faster). 
	- No significant improvement observed in the Lattice case.
	- Result can be found in this [notebook](https://github.com/ODISSEI-School-Choice/school-choice/blob/jisk-v2/profile.ipynb)
- Scaling graph:
	- Result shows a nearly linear time/memory increase when increasing the number of schools/neighborhoods, and a quadratic growth when increasing the number of students.
	- Result can be found in this [notebook](https://github.com/ODISSEI-School-Choice/school-choice/blob/jisk-v2/scaling_graph.ipynb)
