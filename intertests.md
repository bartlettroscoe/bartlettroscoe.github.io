---
layout: page
title: Interests
permalink: /interests/
---

### Software Engineering and Integration for Computational Science and Engineering

Roscoe's current technical interests include applying modern Lean/Agile
software engineering approaches to computational science and engineering
problems including build and test systems
(e.g. [TriBITS](https://tribits.org)), software development and integration
workflows and processes, and software sustainability. His more recent
interests focus on software engineering processes and workflows for creating
packages of sustainable software and sustainable ecosystems of packages shared
among large distributed teams of developers over long periods of time.

### Abstract Numerical Algorithms (ANAs)

An ANA is any numerical algorithm that can be expressed abstractly solely in
terms of vectors, vector spaces, linear operators, and other abstractions
built on top of these without general direct data access or any general
assumptions about data locality.  Roscoe's interest in ANAs is that they can
be implemented in a very general way and can be reused in an amazingly diverse
set of applications.  Roscoe is the the lead developer of the
[Thyra](../publications#thyra_op_vec_2007) package which defines C++
interfaces and support software for the interoperability and development of
ANAs.

### Object-Oriented Software Engineering for Large-Scale Numerics

Roscoe has a general interest in object-oriented methods for large-scale
numerical programming. A number of Trilinos packages (e.g. Belos, Anasazi,
NOX, LOCA ) are ANAs that are implemented in, or accessible through, Thyra
interfaces. The Thyra interface layer has been used to effectively link
together a wide variety numerical algorithmic software ranging from basic
parallel linear algebra (e.g. Tpetra) all the way through transient
sensitivities (e.g. Tempus) and optimization (e.g. ROL and MOOCHO).

### Object-Oriented Programming in C++

Currently, C++ is the language of choice for large-scale, object-oriented
numerical programming. C++ is unique in that it directly supports
object-oriented programming, is close to the hardware (allowing for very high
performance code right out of the box), is standardized, and has a high
availability (including high performance platforms). However, C++ is perhaps
the most complex programming language ever devised in wide-spread use. Roscoe
has a general interest in developing and refining idioms to make
object-oriented numerical programming in C++ safer, more productive, more
general, and more efficient (e.g. [Teuchos Memory Management
Classes](../publications#teuchos_cxx_mem_mng_classes)).
