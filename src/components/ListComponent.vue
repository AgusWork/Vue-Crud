<template>
    <div class="container">
        <SaveComponent :productEdit="product" @productInsert="productInsert" @productUpdate="productUpdate" />
        <div class="products-list">
            <h3 class="list-title">Lista de Productos</h3>
            <ul>
                <li v-for="item in products" :key="item.id" class="product-item">
                    <div class="product-info">
                        <p>Nombre: {{ item.name }}</p>
                        <p>Valor: ${{ item.value.toLocaleString('es-AR') }}</p>
                    </div>
                    <div class="product-actions">
                        <button @click="productEdit(item)" class="edit-btn">Editar</button>
                        <button @click="productDelete(item)" class="delete-btn">Eliminar</button>
                    </div>
                </li>
                <li v-if="!products.length" class="no-items">No hay productos aún.</li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 50vh;
    padding: 20px;
    font-family: 'Roboto', sans-serif;
    max-width: 700px;
    margin: 0 auto;
}

.products-list {
    width: 100%;
    margin-top: 30px;
}

.list-title {
    font-family: 'Poppins', sans-serif;
    font-size: 1.8rem;
    color: #2c3e50;
    text-align: center;
    margin-bottom: 25px;
}

ul {
    list-style: none;
    padding: 0;
}

.product-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #fff;
    border-radius: 15px;
    padding: 15px 20px;
    margin-bottom: 15px;
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.08);
    transition: all 0.3s ease;
}

.product-item:hover {
    transform: scale(1.02);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.12);
}

.product-info {
    flex: 1;
}

.product-info p {
    margin: 5px 0;
    color: #34495e;
    font-size: 1rem;
}

.product-actions {
    display: flex;
    gap: 12px;
}

.edit-btn,
.delete-btn {
    padding: 8px 16px;
    border: none;
    border-radius: 8px;
    font-family: 'Poppins', sans-serif;
    font-size: 0.9rem;
    color: white;
    cursor: pointer;
    transition: background 0.2s ease;
}

.edit-btn {
    background: #3498db;
}

.edit-btn:hover {
    background: #2980b9;
}

.delete-btn {
    background: #e74c3c;
}

.delete-btn:hover {
    background: #c0392b;
}

.no-items {
    text-align: center;
    color: #7f8c8d;
    font-size: 1.1rem;
    font-style: italic;
    padding: 20px;
}
</style>

<script>
import SaveComponent from "./SaveComponent.vue";
export default {
	name: "ListComponent",
	components: {
		SaveComponent,
	},
	data() {
		return {
			products: [],
			product: "",
		};
	},
	created() {
		const storedProducts = localStorage.getItem("products");
		if (storedProducts) {
			this.products = JSON.parse(storedProducts);
		}
	},
	methods: {
		productInsert(product) {
			product.id = this.products.length + 1;
			this.products.push(product);
			localStorage.setItem("products", JSON.stringify(this.products));
		},
		productEdit(product) {
			this.product = product;
		},
		productUpdate(updatedProduct) {
			const index = this.products.findIndex((p) => p.id === updatedProduct.id);
			if (index !== -1) {
				this.products[index] = updatedProduct;
				localStorage.setItem("products", JSON.stringify(this.products));
			}
		},
		productDelete(product) {
			this.products = this.products.filter((p) => p.id !== product.id);
			localStorage.setItem("products", JSON.stringify(this.products));
		},
	},
};
</script>
