# Práctica 2

>#### Cuéllar Ortega Luis Enrique

**Ejercicio: Código para clasificar y/o para clustering.**

Usando como ejemplo el dataset de iris contenido dentro del mismo R, se puede hacer el siguiente código para clasificar todos los datos en training set y test set.


```R
head(iris)
```


<table>
<caption>A data.frame: 6 × 5</caption>
<thead>
	<tr><th></th><th scope=col>Sepal.Length</th><th scope=col>Sepal.Width</th><th scope=col>Petal.Length</th><th scope=col>Petal.Width</th><th scope=col>Species</th></tr>
	<tr><th></th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;fct&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>5.1</td><td>3.5</td><td>1.4</td><td>0.2</td><td>setosa</td></tr>
	<tr><th scope=row>2</th><td>4.9</td><td>3.0</td><td>1.4</td><td>0.2</td><td>setosa</td></tr>
	<tr><th scope=row>3</th><td>4.7</td><td>3.2</td><td>1.3</td><td>0.2</td><td>setosa</td></tr>
	<tr><th scope=row>4</th><td>4.6</td><td>3.1</td><td>1.5</td><td>0.2</td><td>setosa</td></tr>
	<tr><th scope=row>5</th><td>5.0</td><td>3.6</td><td>1.4</td><td>0.2</td><td>setosa</td></tr>
	<tr><th scope=row>6</th><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td><td>setosa</td></tr>
</tbody>
</table>




```R
set.seed(4024) #Definir una semilla aleatoria
```


```R
div = sample(2, nrow(iris), replace=TRUE, prob=c(0.67, 0.33)) #Esto dividirá el dataset 67% train 33% test
```


```R
iris.training = iris[div==1, 1:4] #Clasifica los de training en un dataset

head(iris.training)
```


<table>
<caption>A data.frame: 6 × 4</caption>
<thead>
	<tr><th></th><th scope=col>Sepal.Length</th><th scope=col>Sepal.Width</th><th scope=col>Petal.Length</th><th scope=col>Petal.Width</th></tr>
	<tr><th></th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>3</th><td>4.7</td><td>3.2</td><td>1.3</td><td>0.2</td></tr>
	<tr><th scope=row>4</th><td>4.6</td><td>3.1</td><td>1.5</td><td>0.2</td></tr>
	<tr><th scope=row>5</th><td>5.0</td><td>3.6</td><td>1.4</td><td>0.2</td></tr>
	<tr><th scope=row>6</th><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td></tr>
	<tr><th scope=row>7</th><td>4.6</td><td>3.4</td><td>1.4</td><td>0.3</td></tr>
	<tr><th scope=row>8</th><td>5.0</td><td>3.4</td><td>1.5</td><td>0.2</td></tr>
</tbody>
</table>




```R
iris.test = iris[div==2, 1:4] #Clasifica los de test en su propio dataset.

head(iris.test)
```


<table>
<caption>A data.frame: 6 × 4</caption>
<thead>
	<tr><th></th><th scope=col>Sepal.Length</th><th scope=col>Sepal.Width</th><th scope=col>Petal.Length</th><th scope=col>Petal.Width</th></tr>
	<tr><th></th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>5.1</td><td>3.5</td><td>1.4</td><td>0.2</td></tr>
	<tr><th scope=row>2</th><td>4.9</td><td>3.0</td><td>1.4</td><td>0.2</td></tr>
	<tr><th scope=row>9</th><td>4.4</td><td>2.9</td><td>1.4</td><td>0.2</td></tr>
	<tr><th scope=row>11</th><td>5.4</td><td>3.7</td><td>1.5</td><td>0.2</td></tr>
	<tr><th scope=row>13</th><td>4.8</td><td>3.0</td><td>1.4</td><td>0.1</td></tr>
	<tr><th scope=row>16</th><td>5.7</td><td>4.4</td><td>1.5</td><td>0.4</td></tr>
</tbody>
</table>



>*Todo unificado en una sóla función se vería de la siguiente forma.*


```R
train = function(data) {
  set.seed(4024)
  div = sample(2, nrow(data), replace=TRUE, prob=c(0.67, 0.33))
  data.training = data[div==1, 1:4]
  return(data.training)
}

test = function(data) {
    set.seed(4024)
    div = sample(2,nrow(data), replace=TRUE, prob=c(0.67,0.33))
    data.test = data[div==2, 1:4]
    return(data.test)
}
```


```R
iris.training = train(iris)
head(iris.training)
```


<table>
<caption>A data.frame: 6 × 4</caption>
<thead>
	<tr><th></th><th scope=col>Sepal.Length</th><th scope=col>Sepal.Width</th><th scope=col>Petal.Length</th><th scope=col>Petal.Width</th></tr>
	<tr><th></th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>3</th><td>4.7</td><td>3.2</td><td>1.3</td><td>0.2</td></tr>
	<tr><th scope=row>4</th><td>4.6</td><td>3.1</td><td>1.5</td><td>0.2</td></tr>
	<tr><th scope=row>5</th><td>5.0</td><td>3.6</td><td>1.4</td><td>0.2</td></tr>
	<tr><th scope=row>6</th><td>5.4</td><td>3.9</td><td>1.7</td><td>0.4</td></tr>
	<tr><th scope=row>7</th><td>4.6</td><td>3.4</td><td>1.4</td><td>0.3</td></tr>
	<tr><th scope=row>8</th><td>5.0</td><td>3.4</td><td>1.5</td><td>0.2</td></tr>
</tbody>
</table>




```R
iris.test = test(iris)
head(iris.test)
```


<table>
<caption>A data.frame: 6 × 4</caption>
<thead>
	<tr><th></th><th scope=col>Sepal.Length</th><th scope=col>Sepal.Width</th><th scope=col>Petal.Length</th><th scope=col>Petal.Width</th></tr>
	<tr><th></th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>5.1</td><td>3.5</td><td>1.4</td><td>0.2</td></tr>
	<tr><th scope=row>2</th><td>4.9</td><td>3.0</td><td>1.4</td><td>0.2</td></tr>
	<tr><th scope=row>9</th><td>4.4</td><td>2.9</td><td>1.4</td><td>0.2</td></tr>
	<tr><th scope=row>11</th><td>5.4</td><td>3.7</td><td>1.5</td><td>0.2</td></tr>
	<tr><th scope=row>13</th><td>4.8</td><td>3.0</td><td>1.4</td><td>0.1</td></tr>
	<tr><th scope=row>16</th><td>5.7</td><td>4.4</td><td>1.5</td><td>0.4</td></tr>
</tbody>
</table>



**Finalmente se logra clasificar el dataset en el grupo de training y test para posteriormente pasarlo a la función de k-vecinos cercanos**


```R
iris.traintypes = iris[div==1,5] #Aquí se guardan los tipos de iris que hay en train y test.

iris.testtypes = iris[div==2, 5]
```


```R
library(class) #librería con funcion knn (k-nearest neighbors)
? knn
```



<table width="100%" summary="page for knn {class}"><tr><td>knn {class}</td><td style="text-align: right;">R Documentation</td></tr></table>

<h2>
k-Nearest Neighbour Classification
</h2>

<h3>Description</h3>

<p>k-nearest neighbour classification for test set from training set. For
each row of the test set, the <code>k</code> nearest (in Euclidean distance)
training set vectors are found, and the classification is decided by
majority vote, with ties broken at random. If there are ties for the
<code>k</code>th nearest vector, all candidates are included in the vote.
</p>


<h3>Usage</h3>

<pre>
knn(train, test, cl, k = 1, l = 0, prob = FALSE, use.all = TRUE)
</pre>


<h3>Arguments</h3>

<table summary="R argblock">
<tr valign="top"><td><code>train</code></td>
<td>

<p>matrix or data frame of training set cases.
</p>
</td></tr>
<tr valign="top"><td><code>test</code></td>
<td>

<p>matrix or data frame of test set cases. A vector will be interpreted
as a row vector for a single case.
</p>
</td></tr>
<tr valign="top"><td><code>cl</code></td>
<td>

<p>factor of true classifications of training set
</p>
</td></tr>
<tr valign="top"><td><code>k</code></td>
<td>

<p>number of neighbours considered.
</p>
</td></tr>
<tr valign="top"><td><code>l</code></td>
<td>

<p>minimum vote for definite decision, otherwise <code>doubt</code>. (More
precisely, less than <code>k-l</code> dissenting votes are allowed, even if <code>k</code>
is increased by ties.)
</p>
</td></tr>
<tr valign="top"><td><code>prob</code></td>
<td>

<p>If this is true, the proportion of the votes for the winning class
are returned as attribute <code>prob</code>.
</p>
</td></tr>
<tr valign="top"><td><code>use.all</code></td>
<td>

<p>controls handling of ties. If true, all distances equal to the <code>k</code>th
largest are included. If false, a random selection of distances
equal to the <code>k</code>th is chosen to use exactly <code>k</code> neighbours.
</p>
</td></tr></table>


<h3>Value</h3>

<p>Factor of classifications of test set. <code>doubt</code> will be returned as <code>NA</code>.
</p>


<h3>References</h3>

<p>Ripley, B. D. (1996)
<em>Pattern Recognition and Neural Networks.</em> Cambridge.
</p>
<p>Venables, W. N. and Ripley, B. D. (2002)
<em>Modern Applied Statistics with S.</em> Fourth edition.  Springer.
</p>


<h3>See Also</h3>

<p><code>knn1</code>, <code>knn.cv</code>
</p>


<h3>Examples</h3>

<pre>
train &lt;- rbind(iris3[1:25,,1], iris3[1:25,,2], iris3[1:25,,3])
test &lt;- rbind(iris3[26:50,,1], iris3[26:50,,2], iris3[26:50,,3])
cl &lt;- factor(c(rep("s",25), rep("c",25), rep("v",25)))
knn(train, test, cl, k = 3, prob=TRUE)
attributes(.Last.value)
</pre>

<hr /><div style="text-align: center;">[Package <em>class</em> version 7.3-15 ]</div>



```R
irispred = knn(train = iris.training, test = iris.test, cl = iris.traintypes, k=5)

irispred
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>setosa</li><li>setosa</li><li>setosa</li><li>setosa</li><li>setosa</li><li>setosa</li><li>setosa</li><li>setosa</li><li>setosa</li><li>setosa</li><li>setosa</li><li>setosa</li><li>setosa</li><li>versicolor</li><li>versicolor</li><li>versicolor</li><li>versicolor</li><li>versicolor</li><li>versicolor</li><li>versicolor</li><li>versicolor</li><li>versicolor</li><li>versicolor</li><li>versicolor</li><li>versicolor</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li><li>virginica</li></ol>

<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'setosa'</li><li>'versicolor'</li><li>'virginica'</li></ol>
</details>



```R
irisTesttypes = data.frame(iris.testtypes) #Hace dataset los tipos de iris guardados en test.

both = data.frame(irispred, iris.testtypes) #Combina los datos del tipo de iris predecido y el de test.

names(both) = c("Especies Predecidas", "Especies Observadas") #Nombres de las columnas en el nuevo dataset.

both
```


<table>
<caption>A data.frame: 42 × 2</caption>
<thead>
	<tr><th scope=col>Especies Predecidas</th><th scope=col>Especies Observadas</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th></tr>
</thead>
<tbody>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>setosa    </td><td>setosa    </td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>versicolor</td><td>versicolor</td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
	<tr><td>virginica </td><td>virginica </td></tr>
</tbody>
</table>



**Se puede ver en la tabla anterior que las especies observadas y predecidas son exactamente iguales, logrando una predicción correcta muy eficiente.**
