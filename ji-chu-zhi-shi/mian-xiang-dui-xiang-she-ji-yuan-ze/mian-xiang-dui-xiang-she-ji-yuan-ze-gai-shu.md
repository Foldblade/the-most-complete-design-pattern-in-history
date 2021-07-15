# 面向对象设计原则概述

对于面向对象软件系统的设计而言，在支持可维护性的同时，提高系统的可复用性是一个至关重要的问题，如何同时提高一个软件系统的可维护性和可复用性是面向对象设计需要解决的核心问题之一。在面向对象设计中，可维护性的复用是以设计原则为基础的。每一个原则都蕴含一些面向对象设计的思想，可以从不同的角度提升一个软件结构的设计水平。

面向对象设计原则为支持可维护性复用而诞生，这些原则蕴含在很多设计模式中，它们是从许多设计方案中总结出的指导性原则。面向对象设计原则也是我们用于评价一个设计模式的使用效果的重要指标之一，在设计模式的学习中，大家经常会看到诸如“XXX模式符合XXX原则”、“XXX模式违反了XXX原则”这样的语句。 

最常见的7种面向对象设计原则如下表所示：

 表 1   7 种常用的面向对象设计原则

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x8BBE;&#x8BA1;&#x539F;&#x5219;&#x540D;&#x79F0;</b>
      </th>
      <th style="text-align:left"><b>&#x5B9A;  &#x4E49;</b>
      </th>
      <th style="text-align:left"><b>&#x4F7F;&#x7528;&#x9891;&#x7387;</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>&#x5355;&#x4E00;&#x804C;&#x8D23;&#x539F;&#x5219;</p>
        <p>(Single Responsibility Principle, SRP)</p>
      </td>
      <td style="text-align:left">&#x4E00;&#x4E2A;&#x7C7B;&#x53EA;&#x8D1F;&#x8D23;&#x4E00;&#x4E2A;&#x529F;&#x80FD;&#x9886;&#x57DF;&#x4E2D;&#x7684;&#x76F8;&#x5E94;&#x804C;&#x8D23;</td>
      <td
      style="text-align:left">&#x2605;&#x2605;&#x2605;&#x2605;&#x2606;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x5F00;&#x95ED;&#x539F;&#x5219;</p>
        <p>(Open-Closed Principle, OCP)</p>
      </td>
      <td style="text-align:left">&#x8F6F;&#x4EF6;&#x5B9E;&#x4F53;&#x5E94;&#x5BF9;&#x6269;&#x5C55;&#x5F00;&#x653E;&#xFF0C;&#x800C;&#x5BF9;&#x4FEE;&#x6539;&#x5173;&#x95ED;</td>
      <td
      style="text-align:left">&#x2605;&#x2605;&#x2605;&#x2605;&#x2605;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x91CC;&#x6C0F;&#x4EE3;&#x6362;&#x539F;&#x5219;</p>
        <p>(Liskov Substitution Principle, LSP)</p>
      </td>
      <td style="text-align:left">&#x6240;&#x6709;&#x5F15;&#x7528;&#x57FA;&#x7C7B;&#x5BF9;&#x8C61;&#x7684;&#x5730;&#x65B9;&#x80FD;&#x591F;&#x900F;&#x660E;&#x5730;&#x4F7F;&#x7528;&#x5176;&#x5B50;&#x7C7B;&#x7684;&#x5BF9;&#x8C61;</td>
      <td
      style="text-align:left">&#x2605;&#x2605;&#x2605;&#x2605;&#x2605;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x4F9D;&#x8D56;&#x5012;&#x8F6C;&#x539F;&#x5219;</p>
        <p>(Dependence Inversion Principle, DIP)</p>
      </td>
      <td style="text-align:left">&#x62BD;&#x8C61;&#x4E0D;&#x5E94;&#x8BE5;&#x4F9D;&#x8D56;&#x4E8E;&#x7EC6;&#x8282;&#xFF0C;&#x7EC6;&#x8282;&#x5E94;&#x8BE5;&#x4F9D;&#x8D56;&#x4E8E;&#x62BD;&#x8C61;</td>
      <td
      style="text-align:left">&#x2605;&#x2605;&#x2605;&#x2605;&#x2605;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x63A5;&#x53E3;&#x9694;&#x79BB;&#x539F;&#x5219;</p>
        <p>(Interface Segregation Principle, ISP)</p>
      </td>
      <td style="text-align:left">&#x4F7F;&#x7528;&#x591A;&#x4E2A;&#x4E13;&#x95E8;&#x7684;&#x63A5;&#x53E3;&#xFF0C;&#x800C;&#x4E0D;&#x4F7F;&#x7528;&#x5355;&#x4E00;&#x7684;&#x603B;&#x63A5;&#x53E3;</td>
      <td
      style="text-align:left">&#x2605;&#x2605;&#x2606;&#x2606;&#x2606;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x5408;&#x6210;&#x590D;&#x7528;&#x539F;&#x5219;</p>
        <p>(Composite Reuse Principle, CRP)</p>
      </td>
      <td style="text-align:left">&#x5C3D;&#x91CF;&#x4F7F;&#x7528;&#x5BF9;&#x8C61;&#x7EC4;&#x5408;&#xFF0C;&#x800C;&#x4E0D;&#x662F;&#x7EE7;&#x627F;&#x6765;&#x8FBE;&#x5230;&#x590D;&#x7528;&#x7684;&#x76EE;&#x7684;</td>
      <td
      style="text-align:left">&#x2605;&#x2605;&#x2605;&#x2605;&#x2606;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#x8FEA;&#x7C73;&#x7279;&#x6CD5;&#x5219;</p>
        <p>(Law of Demeter, LoD)</p>
      </td>
      <td style="text-align:left">&#x4E00;&#x4E2A;&#x8F6F;&#x4EF6;&#x5B9E;&#x4F53;&#x5E94;&#x5F53;&#x5C3D;&#x53EF;&#x80FD;&#x5C11;&#x5730;&#x4E0E;&#x5176;&#x4ED6;&#x5B9E;&#x4F53;&#x53D1;&#x751F;&#x76F8;&#x4E92;&#x4F5C;&#x7528;</td>
      <td
      style="text-align:left">&#x2605;&#x2605;&#x2605;&#x2606;&#x2606;</td>
    </tr>
  </tbody>
</table>

 【作者：刘伟  [http://blog.csdn.net/lovelion](http://blog.csdn.net/lovelion)】

