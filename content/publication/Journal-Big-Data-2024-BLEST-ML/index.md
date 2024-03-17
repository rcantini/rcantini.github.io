---
title: "Block size estimation for data partitioning in HPC applications using machine learning techniques"
date: 2024-01-16
publishDate: 2024-01-16
authors: ["Riccardo Cantini", "Fabrizio Marozzo", "Alessio Orsino", "Domenico Talia", "Paolo Trunfio", "Rosa M. Badia", "Jorge Ejarque", "Fernando V. Novoa"]
publication_types: ["2"]
abstract: "The extensive use of HPC infrastructures and frameworks for running data-intensive applications has led to a growing interest in data partitioning techniques and strategies. In fact, application performance can be heavily affected by how data are partitioned, which in turn depends on the selected size for data blocks, i.e. the block size. Therefore, finding an effective partitioning, i.e. a suitable block size, is a key strategy to speed-up parallel data-intensive applications and increase scalability. This paper describes a methodology, namely BLEST-ML (BLock size ESTimation through Machine Learning), for block size estimation that relies on supervised machine learning techniques. The proposed methodology was evaluated by designing an implementation tailored to dislib, a distributed computing library highly focused on machine learning algorithms built on top of the PyCOMPSs framework. We assessed the effectiveness of the provided implementation through an extensive experimental evaluation considering different algorithms from dislib, datasets, and infrastructures, including the MareNostrum 4 supercomputer. The results we obtained show the ability of BLEST-ML to efficiently determine a suitable way to split a given dataset, thus providing a proof of its applicability to enable the efficient execution of data-parallel applications in high performance environments."
featured: true
publication: "*Journal of Big Data*, vol.11, no. 1, pp. 1-23, 2024"
# url_pdf: "..."
doi: "https://doi.org/10.1186/s40537-023-00862-w"
url_project: "https://github.com/rcantini/BLEST-ML"
- name: Amazon
  url: https://github.com/rcantini/BLEST-ML
  icon_pack: fab
  icon: github
# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: ""
  focal_point: ""
  preview_only: false


tags: ["Machine learning", "Big Data analysis", "Data partitioning", High performance computing]
---