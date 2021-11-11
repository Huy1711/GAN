# GAN---Generative-Adversarial-Network-
Implementation of GAN - Generative Adversarial Network 

## Dataset

**MNIST**: Bộ dữ liệu gồm các hình ảnh chữ số viết tay (từ 0 đến 9), tập train gồm 60,000 mẫu, tập test gồm 10,000 mẫu. Mỗi ảnh đều có kích cỡ 28x28 pixel, mỗi pixel chứa 1 giá trị thể hiện độ sáng tối của pixel đó (grayscale). Giá trị càng cao thì càng tối, là một số thực nằm trong khoảng 0 đến 255.

**FashionMNIST**: Bộ dữ liệu gồm các hình ảnh về các phụ kiện, quần áo; tập train gồm 60,000 mẫu, tập test gồm 10,000 mẫu. Mỗi ảnh đều có kích cỡ 28x28 pixel và giá trị grayscale giống với MNIST.

Mỗi mẫu đều được gán với 1 trong các nhãn: 0 T-shirt/top, 1 Trouser, 2 Pullover, 3 Dress, 4 Coat, 5 Sandal, 6 Shirt, 7 Sneaker, 8 Bag, 9 Ankle boot.

## Define the Model

![image](https://user-images.githubusercontent.com/41891935/141313326-aababc39-3632-4137-b22d-12fea6d48858.png)

### Discriminator

Sử dụng mạng MLP, mỗi lớp có hàm kích hoạt là Leaky ReLU

**Leaky ReLu**

![image](https://user-images.githubusercontent.com/41891935/141313366-87e60cc9-772c-4d29-96ca-02b0d09e4a33.png)

**Sigmoid Output**

Discriminator sẽ có giá trị output nằm trong khoảng 0-1 quyết định nhãn *real* hoặc *fake*.

Ta sử dụng hàm loss [BCEWithLogitsLoss](https://pytorch.org/docs/stable/nn.html#bcewithlogitsloss), hàm này bao gồm hàm sigmoid để làm hàm kích hoạt và hàm loss BCE.

**Dropout**

Ta sử dụng Dropout để huấn luyện cả Discriminator và Generator

### Generator

Cũng sử dụng mạng MLP có cấu trúc giống Discriminator nhưng áp dụng thêm hàm *tanh* vào lớp output

**tanh Output**

Hàm *tanh* sẽ làm cho output nằm trong khoảng -1 đến 1, thay vì 0 đến 1.

![image](https://user-images.githubusercontent.com/41891935/141313400-03f4ce4e-81b4-4792-8695-687eaf6895a6.png)

## **Discriminator and Generator Losses**

### **Discriminator Losses**

Đối với discriminator, tổng loss sẽ là `d_loss = d_real_loss + d_fake_loss`

trong đó d_real_loss là loss đối với dữ liệu từ tập dữ liệu huấn luyện, còn d_fake_loss là loss đối với dữ liệu từ Generator.

Ta sử dụng hàm loss binary cross entropy loss with logits (hàm [BCEWithLogitsLoss](https://pytorch.org/docs/stable/nn.html#bcewithlogitsloss)). Hàm này bao gồm hàm sigmoid để làm hàm kích hoạt và hàm loss BCE. Và output của discriminator là 1 cho ảnh real và 0 cho ảnh fake. Ta muốn tối đa $D(x)$ và $1-D(G(z))$

### **Generator Losses**

Latent vector đầu vào sẽ là một vector sinh ngẫu nhiên theo phân phối chuẩn với kỳ vọng bằng 0 và phương sai bằng 1.

Loss của generator được tính bằng real_loss của discriminator đối với ảnh fake. Tức là ta muốn tối đa $D(G(z))$

## **Optimizers**

Sử dụng 2 **Adam optimizers** riêng cho discriminator và generator để cập nhật bộ trọng số của chúng.

## **Training**

Ta huấn luyện lần lượt discriminator và generator.

**Discriminator training**

1. Tính real_loss trên tập dữ liệu ảnh thật (training dataset)
2. Generator sinh ảnh
3. Tính fake_loss trên tập dữ liệu sinh bởi Generator
4. Lấy tổng real_loss và fake_loss
5. Thực hiện Backpropagation và 1 bước tối ưu để cập nhật trọng số của Discriminator

**Generator training**

1. Generator sinh ảnh
2. Tính real_loss của Discriminator trên tập dữ liệu ảnh sinh
3. Thực hiện Backpropagation và 1 bước tối ưu để cập nhật trọng số của Generator
