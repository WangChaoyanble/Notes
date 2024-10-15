# Eyeriss : An Energy-Efficient Reconfigurable Accelerator for Deep Convolutional Neural Networks

## Related abbreviations
- PEs: processing elements
- GLB: global buffer
- NoC: network-on-chip
- RLC: Run-length compression 
- ifmaps: input feature maps
- ofmaps: output feature maps
- psums: patial sums



## Eyeriss system architecture
![alt text](../../assets/MarkdownImg/image-15.png)
- Two clock domains:
  - Core clock domain :for processing.
  - Link clock domain :for communication with the off-chip DRAM.
  - Two domains run independently and communicate through an asynchronous FIFO interface.

- Four levels of memory hierarchy: in decreasing energy per access: DRAM, GLB, inter-PE communication, and spads.
- To transfer data for computation, each PE can communicate with:
  -  Its neighbor PEs
  -  The GLB through an NoC
  -  Spads: a memory space that is local to the PE

## PE architecture
1-D Convolution In a PE: filter row is fixed
![alt text](../../assets/MarkdownImg/image-16.png)
![alt text](../../assets/MarkdownImg/image-14.png)

2-D Convolution in PEs:

![alt text](../../assets/MarkdownImg/image-17.png)

- Filter rows are reused across PEs horizontally.
  ![alt text](../../assets/MarkdownImg/image-18.png)
- Fmap rows are reused across PEs diagnally.
  ![alt text](../../assets/MarkdownImg/image-19.png)
- Partial sums accumulated across PEs veritally.
  ![alt text](../../assets/MarkdownImg/image-20.png)

## Dimensions Beyond 2-D Convolution:
- Multiple Fmaps:
  ![alt text](../../assets/MarkdownImg/image-21.png)
- Multiple Filters:
  ![alt text](../../assets/MarkdownImg/image-22.png)
- Multipel channels: Psum=Psum1+Psum2
  ![alt text](../../assets/MarkdownImg/image-23.png)
- Full picture: Map rows from multiple fmaps, filters and channels to same PE to exploit other forms of reuse and local accumulation
  ![alt text](../../assets/MarkdownImg/image-24.png)


Hardware Architecture: input filter and fmap, output the result fmap

![alt text](../../assets/MarkdownImg/image-25.png)

Data Delivery with NoC:
![alt text](../../assets/MarkdownImg/image-26.png)

Accommodate different shapes with fixed PE array:

![alt text](../../assets/MarkdownImg/image-27.png)






