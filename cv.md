# Pavel Chareichyk

> my e-mail: pavel.gromov.1998@mail.ru  
> my telephone number: +375 (29) 752-18-98  
> Also you can find me in VK: https://vk.com/pavel__chehov  

  I am a 4th year student of the Faculty of Physics of BSU. My specialty is computer physics, which implies modeling of physical processes, which can be very different. However, modeling requires not only a good knowledge of programming, algorithms and the process in particular, but also good imagination, perseverance and zeal.
Also, I am not an exception to the famous expression "Physicist-lyricist" - I am fascinated by literature, art and photography. I believe that this is not something separate from any accuracy and order, because even the driest programming and mathematics are art.

## Education
  I work with programming languages and platforms such as: С++, Mathematica, MathCad, PHP, Vue.js, and now I'm learning to work with CSS and HTML
  
## English
  Unfortunately, my practice of English does not go beyond school and university study.


## Code examples  
#### Wolfram mathematica


    VectorFieldPlot3D[Ed, {x, -10, 10}, {y, -10, 10}, {z, -10, 10},VectorHeads -> True]
    D3 = {-1, 1}
    D4 = {1, -1)
    l1 = D3 + D4
    R0a = {x, y}
    alpha = R0a.D3/(Sqrt[R0a.R0a]*Sqrt[D4.D4])
    er = R0a/Sqrt[R0a.R0a]*alpha
    Ed1 = (er*Cos[alpha]*Sqrt[D4.D4] - l1)/(Sqrt[R0a.R0a]^3)
    Plot3D[Ed1, {x, -20, 20}, {y, -20, 20}
    L1 = {1, 1, -5};
    L2 = {1, 1, 5};
    r1 = R + L1; 
    r2 = R - L2;
    Alpha1 = r1.L1/(Sqrt[r1.r1]*Sqrt[L1.L1]);
    Alpha2 = r2.L2/(Sqrt[r2.r2]*Sqrt[L2.L2]);
    Bmag = Cos[Alpha1] - Cos[Alpha2] 
    SliceContourPlot3D[Bmag, {x, -20, 1}, {y, -20, 1}, {z, -20, 20}]


    L3 = {-2, 1};
    L4 = {1, 3};
    r3 = R0a + L3;
    r4 = R0a - L4;
    Alpha3 = r3.L3/(Sqrt[r3.r3]*Sqrt[L3.L3]);
    Alpha4 = r4.L4/(Sqrt[r4.r4]*Sqrt[L4.L4]);
    Bmag = Cos[Alpha3] - Cos[Alpha4] // Simplify
    Plot3D[Bmag, {x, -20, 20}, {y, -20, 20}]
    
#### C++
    #include <iostream>
    #include "cmath"
    #include "fstream"
    using namespace std;


    double x = 10,  T = 1;  
    double xnull = 2.5;
    double a = 400, t = 5000;   
    const int Nx = 400;
    double dx = x / a, tau = 0.0002;     
    double pi = 3.1415;
    double sigma = 1;
    double A1[Nx], A2[Nx], A3[Nx], B1[Nx], B2[Nx], B3[Nx], U[Nx], AB1[Nx], AB2[Nx], AB3[Nx];
    double gran1 = 6.25, gran2 = 7.5;
    double glyb = 1;
    double a1 = 35.5;
    double a2 = 52.8;
    double a3 = 7.2;
    double a4 = 1;
    double C1 = 2 * tau / (a1 * pow(dx, 2));


    int main() {
	  ofstream file1, file2, file3;
	  file1.open("A1.txt");
	file2.open("B1.txt");
	file3.open("AB.txt");

	double vrem = 2 * tau;
	double temp;
	double K, count = 2;
	for (int i = 0; i <= a - 1; i++) {
		if (i * dx >= gran1) {
			if (i * dx <= gran2) {
				U[i] = glyb;
			}
			else {
				U[i] = 0;
			}
		}
		else {
			U[i] = 0;
		}
		A1[i] = (1 / (pow(pi, 0.25) * pow(sigma, 0.5)))  / (exp(a4 * (pow(i * dx - xnull, 2))));
		B1[i] = (1 / (pow(pi, 0.25) * pow(sigma, 0.5)))  / (exp(a4 * (pow(i * dx - xnull, 2))));
		AB1[i] = pow(A1[i], 2) + pow(B1[i], 2);
		file1 << "{" << i * dx << "," << A1[i] << "},";
		file2 << "{" << i * dx << "," << B1[i] << "},";
		file3 << "{" << i * dx << "," << AB1[i] << "},";
	}

	A1[0] = 0;
	A1[Nx - 2] = 0;
	B1[0] = 0;
	B1[Nx - 2] = 0;

	for (int i = 1; i <= a - 1; i++) {
		A2[i] = A1[i] - (tau / (a1 * pow(dx, 2))) * (B1[i + 1] - 2 * B1[i] + B1[i - 1]) + tau * a2 * U[i] * B1[i] / a1;
		B2[i] = B1[i] + (tau / (a1 * pow(dx, 2))) * (A1[i + 1] - 2 * A1[i] + A1[i - 1]) + tau * a2 * U[i] * A1[i] / a1;
		AB2[i] = pow(A2[i], 2) + pow(B2[i], 2);
		//if (i * dx == xnull && j * dy == ynull) {
		//	cout << endl << AB2[i][j] << endl;
		//}
	}
	for (int i = 1; i <= a - 1; i++) {
		for (int j = 1; j <= b - 1; j++) {
			if (i * dx >= gran1 - dx && i * dx <= gran2 - dx) {
				U[i][j] = glyb;
			}
			else {
				U[i][j] = 0;
			}
			//cout << U[i][j] << endl;
		}
	}
	file3 << endl << "t="<<tau << endl;
	for (int i = 0; i <= a - 1; i++) {
		file3 << "{" << i * dx << "," << AB2[i] << "},";
		}
	while (vrem <= T) {
		//file3 << endl << "t=" << vrem << endl;
		cout << vrem << endl;
		for (int i = 1; i <= a - 1; i++) {
			A3[i] = ((1 - pow(C1, 2)) / (1 + pow(C1, 2))) * A1[i] + (2 * C1) / (1 + pow(C1, 2)) * B1[i] + (pow(C1, 2) / (1 + pow(C1, 2)) * (A2[i - 1] + A2[i + 1])) - (C1 / (1 + pow(C1, 2)) * (B2[i - 1] + B2[i + 1])) + (C1 * pow(dx, 2) * a2 / (1 + pow(C1, 2))) * U[i] * B2[i] - ((C1 * pow(dx, 2) * a2) / (1 + pow(C1, 2))) * U[i] * A2[i];
			B3[i] = ((1 - pow(C1, 2)) / (1 + pow(C1, 2))) * B1[i] - (2 * C1) / (1 + pow(C1, 2)) * A1[i] + C1 / (1 + pow(C1, 2)) * (A2[i - 1] + A2[i + 1]) - (pow(C1, 2) / (1 + pow(C1, 2)) * (B2[i - 1] + B2[i + 1])) - (C1 * pow(dx, 2) * a2 / (1 + pow(C1, 2))) * U[i] * A2[i] - ((C1 * pow(dx, 2) * a2) / (1 + pow(C1, 2))) * U[i] * B2[i];
			AB3[i] = pow(A3[i], 2) + pow(B3[i], 2);
			if (count == 500) {
				file3 << "{"<<i * dx << "," << AB3[i]<<"},";
			}
			if (i * dx == xnull && j * dy == ynull) {
				cout <<endl<< AB3[i][j]<<endl;
			}
		}
		for (int i = 1; i <= a - 1; i++) {
			temp = A2[i];
			A1[i] = temp;
			temp = A3[i];
			A2[i] = temp;
		}
		vrem += tau;
		count++;
	}
	for (int i = 1; i <= a - 1; i++) {
		for (int j = 1; j <= b - 1; j++) {
			if (i * dx >= gran1 - dx * (count - 1) && i * dx <= gran2 - dx * (count - 1)) {
				U[i][j] = glyb;
			}
			else {
				U[i][j] = 0;
			}
		}
	}
    

####Vue.js

    <template>
    <div v-show="!isCreating">
      Title: <input v-model="titleText" type='text'>
      Name: <input v-model="projectText" type='text'>
      <button v-on:click="sendForm()"> Create </button>
      <button v-on:click="closeForm"> Cancel </button>
    </div>
    </template>

    <script>
    export default {
    data() {
    return {
      titleText: '',
      projectText: '',
      isCreating: false,
    };
    },
    methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    sendForm() {
      if (this.titleText.length > 0 && this.projectText.length > 0) {
        const title = this.titleText;
        const project = this.projectText;
        this.$emit('create-todo', {
          title,
          project,
          done: false,
        });
        this.titleText = '';
        this.projectText = '';
        this.isCreating = false;
      }
    },
    },
    };
    </script>



## Experience 

  My experience is in numerous laboratory work on modeling physical processes (mainly in C ++). Also, I learned to work on Vue.js and PHP myself.

## Summary

  As with any physicist, my main goal is to study the world around me. For this, of course, you need to know the mathematics, which is the language of science. However, human "capacities" are not enough for the voluminous calculations that science is now engaged in, whether it is molecular dynamics or quantum chemistry. Math alone is not enough today. Programming required. In this regard, every physicist needs to establish a relationship with a computer, start talking to him in his language.
