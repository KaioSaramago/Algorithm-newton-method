# Algorithm-newton-method
problem solved with Newton Raphson method

#define _CRT_SECURE_NO_WARNINGS //para evitar erros de segurança nas funções
#include<math.h>
#include<stdio.h>
#include<Windows.h>
#include <locale.h> //permite acentuação correta nos prints

/*variáveis globais definidas no enunciado da questão*/
float c = 14000, m = 1200, k = 1250000;

float fx(float n, float p, float x0, float x1, float tol, float so, float Xk)
{
	float result = exp(-n*Xk)*(so*cos(p*Xk) + so*(n / p)*sin(p*Xk));
	return result;
}
float derivadafx(float n, float p, float x0, float x1, float tol, float so, float Xk)
{
	float result = ((-n*exp(-n*Xk)*(so*cos(p*Xk) + so*n / p*sin(p*Xk))) + (exp(-n*Xk)*(-so*sin(p*Xk)*p + so*n*cos(p*Xk))));
	return result;
}
void loop(float n, float p, float x0, float x1, float tol, float so)
{
	float Raiz, Xk = (x0 + x1) / 2,errorelativo;
	for (;;)
	{
		Raiz = Xk - (fx(n, p, x0, x1, tol, so, Xk) / derivadafx(n, p, x0, x1, tol, so, Xk));
		errorelativo = ((Raiz - Xk) / Raiz);
		if (errorelativo < 0)
		{
			errorelativo = -errorelativo;
		}
		if (tol > errorelativo)//caso a tolerancia for maior que o erro relativo,as iterações são interrompidas.
		{
			break;
		}
		Xk = Raiz;
	}
	printf("A aproximação da raiz encontrada foi: %f \n Com precisao de: %.10f\n\n", Raiz, errorelativo);
}
void main()
{
	float tol, x0, x1;
	float n = c / (2 * m), p = sqrt((k / m) - ((c*c) / (4 * m*m)));
	float so = 0.13; //Minha matrícula é: 11511EEL013
	setlocale(LC_ALL, "Portuguese");
	printf("Entre com os valores da tolerância e com o intervalo para cálculo da raiz da equação\n\n");
	printf("Fiz esse programa em C com tradução em português,\nportanto utilize a vírgula(,) ao invés do ponto(.) para valores decimais de tolerância. \n\n");
	printf("Tolerancia:");
	scanf_s("%f", &tol);
	printf("\n X0: ");
	scanf_s("%f", &x0);
	printf("\n X1: ");
	scanf_s("%f", &x1);
	loop(n, p, x0, x1, tol, so);
	system("pause");
}
