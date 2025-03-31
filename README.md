# GAN-based-Model-Inversion-Attack
Here's my record when I was learning about modelinversion attack attacks.

## Model inversion attack
Model Inversion Attack (MIA) is a privacy attack in which an attacker uses a trained model to restore or reconstruct its training data (or similar data) to reveal sensitive information or infer sensitive attributes of private data.Model Inversion Attack (MIA) is a privacy attack in which an attacker uses a trained model to restore or reconstruct its training data (or similar data) to reveal sensitive information or infer sensitive attributes of private data.

It is important to note that it is different from adversarial sample attacks, which focus on generating samples that can deceive the target model (or instruct the target model to make some kind of judgment), so that the generated samples may not tend to the actual samples, but it requires the maximum restoration of the samples that participated in private training, such as the face recognition task reverse attack, which requires the return of a visually meaningful graph.

## Hazards
People are always surprised at the usefulness of such an attack, and the fact that it cannot destroy the target model. Don't be frustrated, I had that idea at the beginning of my studies. However, in countries with a culture of greater attention to the privacy of individuals, they are sensitive to any information that is not authorized by them to be accessed by others. For example, the acquisition of a patient's identity information in a medical diagnosis may result in a loss for them when participating in events such as elections, the reconstruction of facial recognition, although it may not necessarily deceive the target model (because our target is not this), can be used for cyberbullying such as doxing based on the generated real visual face, and it is not difficult to find the person's social account based on the person's picture.

## Type
