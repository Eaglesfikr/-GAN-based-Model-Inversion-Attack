# GAN-based-Model-Inversion-Attack
Here's my record when I was learning about modelinversion attack attacks.

## Model inversion attack
Model Inversion Attack (MIA) is a privacy attack in which an attacker uses a trained model to restore or reconstruct its training data (or similar data) to reveal sensitive information or infer sensitive attributes of private data.Model Inversion Attack (MIA) is a privacy attack in which an attacker uses a trained model to restore or reconstruct its training data (or similar data) to reveal sensitive information or infer sensitive attributes of private data.

It is important to note that it is different from adversarial sample attacks, which focus on generating samples that can deceive the target model (or instruct the target model to make some kind of judgment), so that the generated samples may not tend to the actual samples, but former requires the maximum restoration of the samples that participated in private training, such as the face recognition task reverse attack, which requires the return of a visually meaningful graph.

## Hazards
People are always surprised at the usefulness of such an attack, and the fact that it cannot destroy the target model. Don't be frustrated, I had that idea at the beginning of my studies. However, in countries with a culture of greater attention to the privacy of individuals, they are sensitive to any information that is not authorized by them to be accessed by others. For example, the acquisition of a patient's identity information in a medical diagnosis may result in a loss for them when participating in events such as elections, the reconstruction of facial recognition, although it may not necessarily deceive the target model (because our target is not this), can be used for cyberbullying such as doxing based on the generated real visual face, and it is not difficult to find the person's social account based on the person's picture.

## Type
- Query-based model inversion attacks

- Member inference attacks

- GAN-based model inversion attack [Let's focus on it](##GAN-based-model-inversion-attack)

## GAN-based model inversion attack
- The Secret Revealer: Generative Model-Inversion Attacks Against Deep Neural Networks \[[paper](https://arxiv.org/abs/1911.07135#:~:text=Previous%20attempts%20to%20invert%20neural%20networks%2C%20even%20the,invert%20deep%20neural%20networks%20with%20high%20success%20rates.)\]

- Knowledge-enriched Distributional Model Inversion Attacks \[[paper](https://arxiv.org/abs/2010.04092)\]

- Pseudo Label-Guided Model Inversion Attack via Conditional Generative Adversarial Network \[[paper](https://arxiv.org/abs/2302.09814#:~:text=To%20address%20these%20problems%2C%20we%20propose%20Pseudo%20Label-Guided,pseudo-labels%20to%20guide%20the%20training%20of%20the%20cGAN.)\]

The above three articles are all white-box attacks, mainly because they all use the gradient information of the target model, taking PLG-MI as an example, according to the code \[[REPO](https://github.com/LetheSec/PLG-MI-Attack/blob/main/reconstruct.py)\]

```
z = utils.sample_z(
            bs, args.gen_dim_z, device, args.gen_distribution
        )
        z.requires_grad = True

        optimizer = torch.optim.Adam([z], lr=lr)
...
if z.grad is not None:
                z.grad.data.zero_()
...
optimizer.zero_grad()
inv_loss.backward()        #here is to use the gradient information of the model to update the noise
optimizer.step()
```

## GAN-based black-box model inversion attacks
- Label-Only Model Inversion Attacks via Boundary Repulsion \[[paper](https://arxiv.org/abs/2203.01925)\]
- Re-thinking Model Inversion Attacks Against Deep Neural Networks \[[paper](https://arxiv.org/abs/2304.01669)\]
- Label-Only Model Inversion Attacks via Knowledge Transfer \[[paper](https://arxiv.org/abs/2310.19342)\]
- Unstoppable Attack: Label-Only Model Inversion via Conditional Diffusion Model \[[paper](https://arxiv.org/abs/2307.08424)\]

To solve this problem, gradient information under white-box conditions is needed to optimize the input noise, BREPMI Propose a gradient estimation algorithm to estimate the true gradient and optimize the latent input vector. Other methods, however, use different methods to circumvent them, LOMMA leverages a data-augmented approach that makes it possible to attack only with the final categorical probability distribution.LOKT uses the method of knowledge transfer to train an agent model and perform gradient optimization on the agent model to indirectly approximate the behavior of the black box model. And the label-guided diffusion model of CDM-MI can be well applied to the attack model in pure label-only MIA.

## Evaluate metrics

| methods/Evaluate metrics                              | EMI  | GMI | KED-MI | PLG-MI | LOMMA | BREPMI | MIRROR | CDM-MI | LOKT |
|----------------------------------------------|------|-----|--------|--------|-------|--------|--------|--------|------|
| ATTACK ACC                                  |      | ✔   |  ✔     |  ✔     | ✔     | ✔      |  ✔     | ✔      |  ✔   |
| KNN.DIST                                    |      | ✔   |   ✔    | ✔      | ✔     |        |        | ✔      |  ✔   |
| FEAT.DIST                                   |      | ✔   |        |        |       |        |  ✔     |        |      |
| FID                                         |      |     |   ✔    |    ✔   |       |        |        |   ✔    |      |
| PSNR                                        |      |  ✔  |        |        |       |        |        |        |      |
| Attack runtime                              | ✔    |     |        |        |       |        |        |        |      |
| Model accuracy                              | ✔    |     |        |        |       |        |   ✔    |        |      |
| Query Budget                                |      |     |        |        |       |  ✔     |        |        |      |
| sampling strategies                         |      |     |        |        |       | ✔      |        |        |      |
| NIQE                                        |      |     |        |        |       |        | ✔      |        |      |
| Human Study                                 | ✔    |     |        |        |       |        |  ✔      |        |      |
| LPIPS                                       |      |     |        |        |       |        |        | ✔       |     |

*Note*: The attack acc here is the input function is similar to that of the target model, and the classification results of the high-performance model are generally divided into TOP1 and TOP5

## acknowledgment
https://github.com/LetheSec/PLG-MI-Attack
https://github.com/ffhibnese/Model-Inversion-Attack-ToolBox
