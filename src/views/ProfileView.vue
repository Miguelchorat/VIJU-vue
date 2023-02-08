<template>
    <main class="main">
        <header className="main__header">
            <h2 className="main__header__title">MI CUENTA</h2>    
            <img className="main__header__bg" src="/src/assets/img/background.png" />     
            <div className="main__header__blur" />
        </header>
        <section className="main__profile">
            <h3 className="main__profile__title">NOMBRE DE USUARIO</h3>
            <p className="main__profile__text">Sleykun</p>
            <h3 className="main__profile__title">CORREO</h3> 
            <p className="main__profile__text">PLACEHOLDER@correo.com</p>
            <h3 className="main__profile__title">FECHA DE NACIMIENTO</h3>
            <p className="main__profile__text">01/01/1970</p>  
            <input type='button' className="main__profile__button" value="MODIFICAR" />
        </section>
  </main>
</template>