<template>
  <b-container style=" background: #2abd5b; text-align: center; justify-content: center;">
    <b-row>
      <b-col style="padding: 5%;">
        <ul class="tools">
          <li class="water">
            <b-badge variant="primary"></b-badge>
          </li>
          <li class="txt">+</li>
          <li class="millet">
            <b-badge variant="warning"></b-badge>
          </li>
          <li class="txt">=</li>
          <li class="flour">
            <b-badge variant="primary"></b-badge>
          </li>
        </ul>
      </b-col>
    </b-row>
  </b-container>
</template>



<style>
.tools {
  list-style: none;
  display: inline-flex;
}
.tools li {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: #35495e 3px solid;
}
.tools li.txt {
  border: none;
  line-height: 80px;
  color: #fff;
  font-size: 200%;
}
.tools li.water {
  background: #fff  no-repeat center center/cover;
}
.tools li.millet {
  background: #fff  no-repeat center center/cover;
}
.tools li.flour {
  background: #fff  no-repeat center center/cover;
}
</style>
