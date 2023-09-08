
Physics-informed neural networks for transcranial ultrasound wave propagation
10.1016/j.ultras.2023.107026

Transcranial ultrasound imaging has been playing an increasingly important role in the non-invasive treatment of brain disorders. However, the conventional mesh-based numerical wave solvers, which are an integral part of imaging algorithms, suffer from limitations such as high computational cost and discretization error in predicting the wavefield passing through the skull. In this paper, we explore the use of physics-informed neural networks (PINNs) for predicting the transcranial ultrasound wave propagation. The wave equation, two sets of time snapshots data and a boundary condition (BC) are embedded as physical constraints in the loss function during training. The proposed approach has been validated by solving the two-dimensional (2D) acoustic wave equation under three increasingly complex spatially varying velocity models. Our cases demonstrate that due to the meshless nature of PINNs, they can be flexibly applied to different wave equations and types of BCs. By adding physics constraints to the loss function, PINNs can predict wavefields far outside the training data, providing ideas for improving the generalization capability of existing deep learning methods. The proposed approach offers exciting perspectives because of the powerful framework and simple implementation. We conclude with a summary of the strengths, limitations and further research directions of this work.


Wave Equation Modeling via Physics-Informed Neural Networks: Models of Soft and Hard Constraints for Initial and Boundary Conditions
10.3390/s23052792

Therapeutic ultrasound waves are the main instruments used in many noninvasive clinical procedures. They are continuously transforming medical treatments through mechanical and thermal effects. To allow for effective and safe delivery of ultrasound waves, numerical modeling methods such as the Finite Difference Method (FDM) and the Finite Element Method (FEM) are used. However, modeling the acoustic wave equation can result in several computational complications. In this work, we study the accuracy of using Physics-Informed Neural Networks (PINNs) to solve the wave equation when applying different combinations of initial and boundary conditions (ICs and BCs) constraints. By exploiting the mesh-free nature of PINNs and their prediction speed, we specifically model the wave equation with a continuous time-dependent point source function. Four main models are designed and studied to monitor the effects of soft or hard constraints on the prediction accuracy and performance. The predicted solutions in all the models were compared to an FDM solution for prediction error estimation. The trials of this work reveal that the wave equation modeled by a PINN with soft IC and BC (soft-soft) constraints reflects the lowest prediction error among the four combinations of constraints.


Physics-Informed Deep-Learning For Elasticity: Forward, Inverse, and Mixed Problems
10.1002/advs.202300439
Elastography is a medical imaging technique used to measure the elasticity of tissues by comparing ultrasound signals before and after a light compression. The lateral resolution of ultrasound is much inferior to the axial resolution. Current elastography methods generally require both axial and lateral displacement components, making them less effective for clinical applications. Additionally, these methods often rely on the assumption of material incompressibility, which can lead to inaccurate elasticity reconstruction as no materials are truly incompressible. To address these challenges, a new physics-informed deep-learning method for elastography is proposed. This new method integrates a displacement network and an elasticity network to reconstruct the Young's modulus field of a heterogeneous object based on only a measured axial displacement field. It also allows for the removal of the assumption of material incompressibility, enabling the reconstruction of both Young's modulus and Poisson's ratio fields simultaneously. The authors demonstrate that using multiple measurements can mitigate the potential error introduced by the "eggshell" effect, in which the presence of stiff material prevents the generation of strain in soft material. These improvements make this new method a valuable tool for a wide range of applications in medical imaging, materials characterization, and beyond.









