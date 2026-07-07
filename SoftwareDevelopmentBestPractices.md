# Software Development Best Practices for the AuScope Community

## Summary

This document describes best practices that software that is part of the AuScope collection must meet:

- **Minimum Best Practices** are the minimum that we expect all software to meet.
- **Standard Best Practices** are the suite of standards AuScope software should be following. If the software falls short of these standards, developers should have a plan of active development to achieve this level.
- **Target Best Practices** should be considered in the development plan for software under active development.

A [quick reference](SoftwareDevelopmentBestPracticesTable.md) summary table is also available.

<!-- A sample repository that demonstrates these best practices can be found in the [AuScope software template repository](https://github.com/auscope/software_template).-->

---

## Minimum Best Practices

*Practices that codes must follow in order to be accepted by AuScope.*

1. **Licensing**
   1. Use an [Open Source Initiative](https://opensource.org/license) open source license.
      <details>
      <summary>Examples</summary>
      GPL, MIT, BSD
      </details>

2. **Version control**
   1. Use version control to manage code changes.
   2. Use a public repository that is accessible without registration.
      <details>
      <summary>Examples</summary>
      GitHub, GitLab
      </details>
   3. Obtain persistent identifiers versions of the software i.e. 1.3, 7.1.3.

3. **Portability, configuration, and building**
   1. Ensure that the code builds on Unix-like machines (Linux, macOS) with only free tools.
   2. Use a portable build system.
      <details>
      <summary>Examples</summary>
      cmake, make, pixi, etc.
      </details>

4. **Testing**
   1. The software includes tests to verify that it runs properly.
   2. The software reports the results of accuracy and/or established community performance benchmarks.

5. **Documentation**
   1. Describe the research problem the software is designed to address. Discuss significant limitations.
   2. Provide instructions for building and installing the software.
   3. Describe all parameters including units. If dimensionless, specify the scaling used.
   4. Explain the physics the software simulates.
   5. Illustrate how to use the software to solve scientific problems with a few cookbook examples that have sample, editable input files.
   6. Provide documentation online or offline.
   7. Include how to cite the software e.g. CITATION.cff.

6. **Citable publication**
   1. Provide a citable publication.

7. **Support**
   1. Clearly indicate if the software is actively supported and if so, how to report issues, contribute modifications and get help.
      <details>
      <summary>Example</summary>
      Provide a CONTRIBUTING.md document.
      </details>

---

## Standard Best Practices

*Practices in addition to the [Minimum Best Practices](#minimum-best-practices) above that should be used by all software developed within the AuScope community. Software not meeting all standards should be actively working to eliminate deficiencies.*

1. **Version control**
   1. Limit source tree to files necessary to build software, documentation, and run verification tests.
   2. In each release, include release notes distinguishing between significant changes, new features and bugfixes.
      <details>
      <summary>Example</summary>
      Use a changelog following <https://keepachangelog.com/en/1.1.0/>
      </details>

2. **Coding**
   1. Use user-friendly specification of parameters outside of source code. Parameters should be specified at runtime, not at compile time.
      <details>
      <summary>Examples</summary>
      Graphical user interfaces, human readable parameter files.
      </details>
   2. Provide a development plan, updated yearly, with prioritization of new features and an estimated timetable for their implementation.
      <details>
      <summary>Examples</summary>
      Use of GitHub [Milestones](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/creating-and-editing-milestones-for-issues-and-pull-requests)
      </details>
   3. Use comments in the software that describe the following:
      1. Algorithms with appropriate references.
      2. Purpose of functions, objects, etc. and descriptions of arguments (inputs / outputs), and groups of objects.
   4. Strive for a modular design:
      1. Balance the use of external libraries to maximize reuse while minimizing dependencies and maintenance.
         <details>
         <summary>Examples</summary>
         PETSc, deal.II
         </details>
      2. Allow users to extend the code with new features or alternative implementations without destroying original functionality or modifying the main branch.
   5. Use error trapping strategies:
      1. User errors should result in a message that helps the user correct the problem. User errors should not result in crashes without error messages.
      2. Internal errors are generally bugs or unintended uses. Use consistency checks to catch internal errors which generate error messages that help the developer fix the problem.
   6. Aim for scalability:
      1. Use distributed/parallel data structures.
      2. Use messages to transfer information between processes instead of the filesystem.
         <details>
         <summary>Example</summary>
         MPI
         </details>

3. **Portability, configuration, and building**
   1. Build system should verify that appropriate dependencies are available.
      <details>
      <summary>Examples</summary>
      pixi.lock, conda-lock.yml, etc.
      </details>
   2. Use an automated and portable configuration and build system.
   3. Output all configuration and build options during runtime to facilitate reproducibility.
      <details>
      <summary>Examples</summary>
      Commit ID, compiler options, checksum.
      </details>

4. **Testing**
   1. Include pass/fail tests that verify that the software runs properly.
   2. Create a development pipeline that uses continuous integration (CI) to automate running tests.
      <details>
      <summary>Examples</summary>
      GitLab pipelines, GitHub workflows, Azure pipelines, Jenkins.
      </details>

5. **Documentation**
   1. Provide user documentation that describes workflows for research use.
   2. Provide developer documentation that explains how to extend the code in anticipated ways.
   3. Provide documentation in dynamic form and available offline.
      <details>
      <summary>Example</summary>
      Sphinx combined with a PDF file.
      </details>
   4. Illustrate how to use the software to solve major scientific use cases with cookbook examples that have sample, editable input files.
   5. List authors and contributors.
      <details>
      <summary>Example</summary>
      Include a CITATION.cff file.
      </details>

6. **User workflow**
   1. Ensure that running different simulations does not require rebuilding.
   2. Ensure that the code uses user specified directories and filenames for input and output.
   3. Use standard binary file formats.
      <details>
      <summary>Examples</summary>
      NetCDF, HDF5, VTK.
      </details>

---

## Target Best Practices

*Practices in addition to the [Standard Best Practices](#standard-best-practices) above that describe and define long-term development priorities for software developed within the AuScope community. These go beyond the Standard Best Practices and are important for long-term projects.*

1. **Version control**
   1. Add new features in separate branches.
   2. Use a stable development (or main) branch for rapid release of new features.

2. **Coding**
   1. Implement functionality as a library rather than an application.
      1. Leverage alternative implementations via plugins.
      2. Construct higher level applications using libraries as building blocks.
   2. Output provenance information (such as parameters/input script used).
   3. Strive for scalability.
      1. Use parallel access to inputs and outputs.
         <details>
         <summary>Example</summary>
         HDF5, mpi4py
         </details>
   4. Implement checkpointing and restart capability.

3. **Portability, configuration, and building**
   1. Let users select compilers, optimization and additional build flags during configuration without modifying files under version control.
   2. Permit multiple builds using the same source tree.
   3. Ensure software can be installed to a central location.
   4. Make software available as a package and/or containerized application that does not require manual build steps.
   5. Provide executable software via an online portal.
      <details>
      <summary>Examples</summary>
      Jupyter servers, online software gateways.
      </details>

4. **Testing**
   1. Provide pass/fail unit testing for software verification at a fine grain level.
   2. Use the Method of Manufactured Solutions for software verification at a coarse grain level.
   3. Use code coverage tools to assess gaps in test coverage.
      <details>
      <summary>Examples</summary>
      python-coverage and gcov.
      </details>

5. **Documentation**
   1. Include guidelines on parameter scales/combinations for which software is designed/tested.
   2. Provide a list of publications that cite or use the software.
      <details>
      <summary>Examples</summary>
      Link to the citations tracked by AuScope and/or by the project.
      </details>
   3. List ORCIDs for each author and contributor and encourage all contributors to add their ORCID ID to their GitHub profile.
   4. Create a wiki, FAQ, or knowledge base that provides answers to common questions.
   5. Provide guidance on archiving model data for publishing.

6. **User workflow**
   1. Allow for reproducibility via archiving of workflows.
