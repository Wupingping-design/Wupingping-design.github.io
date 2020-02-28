# Wupingping-design.github.io
人脸识别源代码
i=imread('xiaoju1.jpg');
I=rgb2gray(i);        
BW=im2bw(I);             
figure;
imshow(BW);
[n1, n2]=size(BW);
a=floor(n1/20);
b=floor(n2/20);
x1=1;x2=a;
c=a*b;

for i=1:10
    y1=1;y2=b;
    for j=1:10
        if(y2<=b || y2>=9*b) || (x1==1 || x2==a*10)
            loc=find(BW(x1:x2,y1:y2)==0);
            [f, g]=size(loc);
            pr=f*100/c;
            if pr<=100
                BW(x1:x2,y1:y2)=0;
                r1=x1;r2=x2;s1=y1;s2=y2;
                pr1=0;
            end
            imshow(BW);
        end
        y1=y1+b;
        y2=y2+b;
    end
    x1=x1+a;
    x2=x2+b;
end
figure(2)
subplot(1,2,1);
imshow(BW)
title('图像处理');
L=bwlabel(BW,8);
BB=regionprops(L,'BoundingBox');
BB1=struct2cell(BB);
BB2=cell2mat(BB1);

[s1, s2]=size(BB2);
mx=0;
for k=3:4:s2-1
    g=BB2(1,k)*BB2(1,k+1);
    if g>mx && (BB2(1,k)/BB2(1,k+1))<1.6
        mx=g;
        j=k;
    end
end
subplot(1,2,2);
title('人脸识别');
imshow(I);
hold on;
rectangle('Position',[BB2(1,j-2),BB2(1,j-1),BB2(1,j),BB2(1,j)],'EdgeColor','b')
